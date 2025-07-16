# Solución: Navegación entre Stacks Anidados en Expo Router

## Task Information
- **Type**: task
- **Context**: Navigation between nested stacks in Expo Router
- **Stack**: react-native-expo-router
- **Priority**: high
- **Description**: Navigation between nested stacks in Expo Router
- **Requirements**:
  - [ ] Navigation between nested stacks in Expo Router

## Objectives
- Implement navigation between nested stacks in Expo Router
- Follow the expo router documentation

## Requirements
- [ ] Navigation between nested stacks in Expo Router

## Rules to apply
- code-quality.mdc [.cursor/rules/core/code-quality.mdc]
- code-security.mdc [.cursor/rules/core/code-security.mdc]
- code-linting-guidelines.mdc [.cursor/rules/core/code-linting-guidelines.mdc]
- documentation-guidelines.mdc [.cursor/rules/core/documentation-guidelines.mdc]
- project-structure.mdc [.cursor/rules/core/project-structure.mdc]
- locale-configuration.mdc [.cursor/rules/core/locale-configuration.mdc]
- development.mdc [.cursor/rules/core/development.mdc]

## Resumen del Problema

Durante el desarrollo de la aplicación MedTrack, identificamos un problema crítico con la navegación entre rutas anidadas en Expo Router. Los botones de retroceso no funcionaban correctamente cuando se navegaba entre diferentes secciones de la aplicación (tasks → treatments, tasks → health-records, etc.).

### Síntomas del Problema

1. **Headers duplicados**: Se mostraban múltiples barras de navegación apiladas
2. **Botones de retroceso no funcionales**: El botón nativo de "back" no aparecía o no funcionaba correctamente

## Análisis del Problema

### Estructura Original Problemática

```
home/
├── _layout.tsx (Stack principal)
├── tasks/
│   ├── _layout.tsx (Stack independiente)
│   └── [id]/
│       └── _layout.tsx (Stack independiente)
├── treatments/
│   ├── _layout.tsx (Stack independiente)
│   └── [id]/
│       └── _layout.tsx (Stack independiente)
└── health-records/
    ├── _layout.tsx (Stack independiente)
    └── [id]/
        └── _layout.tsx (Stack independiente)
```

### Causa Raíz

Cada carpeta con su propio `_layout.tsx` que contenía un `<Stack>` creaba un **stack de navegación independiente**. Cuando se navegaba entre rutas de diferentes stacks, Expo Router no podía mantener un historial coherente, resultando en:

- Múltiples stacks apilados
- Botones de retroceso no funcionales
- Comportamiento de navegación impredecible

## Solución Implementada

### 1. Unificación del Stack Principal

**Antes:**

```tsx
// home/_layout.tsx
export default function HomeLayout() {
  return (
    <PatientTasksProvider>
      <Stack>
        <Stack.Screen name="index" options={{ headerShown: false }} />
        <Stack.Screen name="tasks" options={{ headerShown: false }} />
        <Stack.Screen name="treatments" options={{ title: t('treatments') }} />
      </Stack>
    </PatientTasksProvider>
  );
}
```

**Después:**

```tsx
// home/_layout.tsx
export default function HomeLayout() {
  const { t } = useTranslation(translations);

  return (
    <PatientTasksProvider>
      <Stack>
        <Stack.Screen name="index" options={{ headerShown: false, title: 'Home' }} />
        <Stack.Screen name="tasks/index" options={{ headerShown: false }} />
        <Stack.Screen name="tasks/[id]/index" options={{ title: t('detailsMedication') }} />
        <Stack.Screen name="treatments/index" options={{ title: t('treatments') }} />
        <Stack.Screen name="treatments/[id]/index" options={{ title: t('detailsMedication') }} />
        <Stack.Screen
          name="health-records/index"
          options={{ title: t('patient.health_record.title') }}
        />
        <Stack.Screen name="health-records/[id]/index" options={{ headerShown: false }} />
        <Stack.Screen name="doctors" options={{ title: t('doctorsList') }} />
      </Stack>
    </PatientTasksProvider>
  );
}
```

### 2. Eliminación de Stacks Anidados

**Eliminamos todos los `<Stack>` de los layouts de subcarpetas:**

```tsx
// home/treatments/[id]/_layout.tsx
export default function MedicationDetailsLayout() {
  const { t } = useTranslation(translations);

  return (
    // Sin Stack wrapper - solo el contenido
    <View>{/* Container de la pantalla */}</View>
  );
}
```

### 3. Navegación con Rutas Relativas al Stack

**Concepto Clave: Navegación Relativa al Stack Independiente**

Cuando navegamos desde `home/tasks/index` hacia otras rutas dentro del mismo stack (`home`), utilizamos rutas relativas que comienzan con `/home/` en lugar de rutas absolutas completas. Esto es fundamental para mantener la coherencia del historial de navegación.

#### ¿Por qué usamos rutas relativas?

**Estructura de rutas en la aplicación:**

```
app/
├── (private)/
│   └── (patient)/
│       └── home/          ← Stack independiente
│           ├── _layout.tsx
│           ├── tasks/
│           ├── treatments/
│           └── health-records/
```

**Navegación CORRECTA (rutas relativas al stack):**

```tsx
// ✅ CORRECTO: Navegación relativa al stack 'home'
router.navigate({
  pathname: '/home/treatments/[id]',
  params: { id: task.entityId },
});

router.navigate({
  pathname: '/home/health-records/create',
});
```

**Navegación INCORRECTA (rutas absolutas):**

```tsx
// ❌ INCORRECTO: Ruta absoluta completa
router.navigate({
  pathname: '/(private)/(patient)/home/treatments/[id]',
  params: { id: task.entityId },
});
```

#### Ventajas de usar rutas relativas:

1. **Historial coherente**: Expo Router mantiene el historial dentro del mismo stack
2. **Botones de retroceso funcionales**: El botón nativo funciona correctamente
3. **Navegación más limpia**: No necesitas conocer la estructura completa de rutas
4. **Mantenibilidad**: Si cambias la estructura de rutas, solo actualizas las rutas relativas

#### Implementación de Navegación desde Tasks

```tsx
// components/custom/task/task-navigation.tsx
export const navigateFromTaskToResource = (task: TaskItem) => {
  if (task.type === 'medication' && task.entityId) {
    router.navigate({
      pathname: '/home/treatments/[id]',
      params: { id: task.entityId },
    });
    return;
  }

  if (task.type === 'health-parameter') {
    if (task.status !== 'completed') {
      // ✅ Navegación relativa al stack 'home'
      router.navigate({
        pathname: '/home/health-records/create',
      });
      return;
    }

    if (task.status === 'completed') {
      // ✅ Navegación relativa al stack 'home'
      router.navigate({
        pathname: '/home/health-records/[id]',
        params: { id: task.entityId },
      });
      return;
    }
  }
};
```

### 4. Componente TaskItem con Navegación

```tsx
// components/custom/task/task-list.tsx
const TaskItem = ({ task, onPress }: { task: TaskItem; onPress?: () => void }) => {
  const handlePress = () => {
    if (onPress) {
      onPress();
    } else {
      navigateFromTaskToResource(task);
    }
  };

  return (
    <TouchableOpacity activeOpacity={0.85} onPress={handlePress}>
      {/* Contenido del componente */}
    </TouchableOpacity>
  );
};
```

## Resultados Obtenidos

### ✅ Problemas Resueltos

1. **Headers únicos**: Solo se muestra una barra de navegación por pantalla
2. **Botones de retroceso funcionales**: El botón nativo funciona correctamente
3. **Navegación consistente**: Comportamiento uniforme desde cualquier origen
4. **Historial coherente**: Expo Router mantiene el historial de navegación correctamente
5. **Warnings eliminados**: Se resolvieron los warnings de "extraneous routes" en el TabNavigator

### ✅ Funcionalidades Verificadas

- [x] Navegación desde `home/tasks/index` hacia `home/treatments/[id]`
- [x] Navegación desde `home/tasks/index` hacia `home/health-records/[id]`
- [x] Botones de retroceso funcionando en todas las rutas
- [x] Eliminación de warnings de rutas duplicadas en TabNavigator
- [ ] Navegación desde notificaciones push (pendiente de prueba)

## Problema Adicional Resuelto: Warnings de "Extraneous Routes"

### Síntomas del Problema

Durante la implementación de la solución principal, aparecieron warnings repetitivos:

```
WARN [Layout children]: Too many screens defined. Route "notifications" is extraneous.
WARN [Layout children]: Too many screens defined. Route "patient/health-record" is extraneous.
WARN [Layout children]: Too many screens defined. Route "patient/treatments/index" is extraneous.
WARN [Layout children]: Too many screens defined. Route "patient/treatments/[id]" is extraneous.
WARN [Layout children]: Too many screens defined. Route "patient/treatments/layout" is extraneous.
WARN [Layout children]: Too many screens defined. Route "patient/treatments/create" is extraneous.
WARN [Layout children]: Too many screens defined. Route "patient/doctors/index" is extraneous.
```

### Análisis del Problema

Los warnings se originaban en el `TabNavigator.tsx` donde se habían definido rutas que:

1. **Estaban duplicadas**: Definidas tanto en `home/_layout.tsx` como en `TabNavigator.tsx`
2. **No existían físicamente**: Algunas rutas no tenían archivos correspondientes
3. **Estaban mal ubicadas**: Rutas que pertenecían a stacks anidados estaban definidas en el nivel de tabs

### Estructura Problemática en TabNavigator

```tsx
// ❌ PROBLEMÁTICO: Rutas duplicadas y mal ubicadas
<Tabs.Screen name="notifications" options={{ href: null }} />
<Tabs.Screen name="patient/health-record" options={{ href: null }} />
<Tabs.Screen name="patient/treatments/index" options={{ href: null }} />
<Tabs.Screen name="patient/treatments/[id]" options={{ href: null }} />
<Tabs.Screen name="patient/treatments/layout" options={{ href: null }} />
<Tabs.Screen name="patient/treatments/create" options={{ href: null }} />
<Tabs.Screen name="patient/doctors/index" options={{ href: null }} />
```

### Solución Implementada

**Principio Claro de Separación de Responsabilidades:**

- **Tabs**: Solo para las rutas principales de navegación por pestañas
- **Stacks**: Para las rutas anidadas dentro de cada tab
- **No duplicar**: Una ruta debe estar definida en un solo lugar

**TabNavigator Limpio:**

```tsx
export const PatientTabNavigator = () => {
  const { t } = useTranslation(translations);
  const { user } = useAuth();
  const { unreadCount } = useNotifications();

  const pathname = usePathname();

  const hideTabs = ['/home/treatments/[id]', '/home/tasks/index'];
  const shouldHideTabs = hideTabs.some((route) => pathname.startsWith(route));

  return (
    <Tabs
      screenOptions={{
        tabBarActiveTintColor: '#007AFF',
        tabBarInactiveTintColor: 'gray',
        tabBarStyle: {
          paddingBottom: 5,
          paddingTop: 5,
          height: 60,
          display: shouldHideTabs ? 'none' : 'flex',
        },
        headerShown: false,
      }}
    >
      {/* ✅ Solo las rutas principales de tabs */}
      <Tabs.Screen
        name="home"
        options={{
          tabBarLabel: t('home'),
          tabBarIcon: ({ color, size }) => <Home color={color} size={size} />,
          headerShown: false,
          title: t('home'),
        }}
      />
      <Tabs.Screen
        name="calendar"
        options={{
          tabBarLabel: t('calendar'),
          tabBarIcon: ({ color, size }) => <Calendar color={color} size={size} />,
          headerShown: false,
          title: t('calendar'),
        }}
      />
      <Tabs.Screen
        name="notifications/index"
        options={{
          tabBarLabel: t('notifications'),
          tabBarIcon: ({ size, focused }) => {
            // ... lógica del icono
          },
          headerShown: false,
          title: t('notifications'),
        }}
      />
      <Tabs.Screen
        name="settings"
        options={{
          tabBarLabel: t('settings'),
          tabBarIcon: ({ color, size }) => <Settings color={color} size={size} />,
          headerShown: false,
        }}
      />
      <Tabs.Screen
        name="profile"
        options={{
          tabBarLabel: t('profile'),
          tabBarIcon: ({ color, size }) => (
            <UserAvatar
              user={user || { firstName: '', lastName: '', profilePicture: '' }}
              size={size + 6}
              onPress={() => {
                router.push('/(private)/(patient)/profile');
              }}
            />
          ),
          headerShown: false,
        }}
      />

      {/* ✅ Solo rutas de onboarding que necesitan estar ocultas */}
      <Tabs.Screen
        name="onboarding/index"
        options={{
          href: null,
          tabBarStyle: { display: 'none' },
        }}
      />
      {/* ... otras rutas de onboarding */}
    </Tabs>
  );
};
```

### Rutas Eliminadas del TabNavigator

**Rutas que se eliminaron porque estaban duplicadas o mal ubicadas:**

- ❌ `notifications` (duplicado con `notifications/index`)
- ❌ `patient/health-record` (no existe o está mal ubicada)
- ❌ `patient/treatments/index` (ya está en `home/_layout.tsx`)
- ❌ `patient/treatments/[id]` (ya está en `home/_layout.tsx`)
- ❌ `patient/treatments/layout` (no debería estar en tabs)
- ❌ `patient/treatments/create` (ya está en `home/_layout.tsx`)
- ❌ `patient/doctors/index` (ya está en `home/_layout.tsx`)

### Resultado

- ✅ **Warnings eliminados**: No más mensajes de "extraneous routes"
- ✅ **Arquitectura limpia**: Separación clara entre tabs y stacks
- ✅ **Navegación consistente**: Cada ruta definida en un solo lugar
- ✅ **Mantenibilidad mejorada**: Estructura más fácil de entender y mantener

## Documentación de Referencia

### Expo Router - Nested Navigators

Según la [documentación oficial de Expo Router sobre navegadores anidados](https://docs.expo.dev/router/advanced/nesting-navigators/):

> "Nesting navigators allow rendering a navigator inside the screen of another navigator."

Esta documentación confirma que los navegadores anidados son una característica fundamental de Expo Router, lo que explica por qué teníamos múltiples stacks independientes en nuestra estructura original.

### Expo Router - Common Navigation Patterns

Según la [documentación de patrones de navegación comunes](https://docs.expo.dev/router/basics/common-navigation-patterns/):

> "If the typical starting point for your app is a set of tabs, but one or more tabs may have more than one screen associated with it, nesting a stack navigator inside of a tab is often the way to go."

Esta cita confirma que el patrón de anidar stacks dentro de otras estructuras de navegación es una práctica común, pero también explica por qué puede llevar a problemas de navegación cuando no se maneja correctamente.

### Expo Router - Stack Navigation

Según la [documentación oficial de Expo Router](https://docs.expo.dev/versions/latest/sdk/router/), Expo Router está construido sobre React Navigation y proporciona navegación basada en archivos para aplicaciones React Native y web.

### Referencias Adicionales

- [Expo Router Documentation](https://docs.expo.dev/versions/latest/sdk/router/)
- [Common Navigation Patterns](https://docs.expo.dev/router/basics/common-navigation-patterns/)
- [Nesting Navigators](https://docs.expo.dev/router/advanced/nesting-navigators/)
- [React Navigation Stack Navigator](https://reactnavigation.org/docs/stack-navigator/) (base de Expo Router)
- [Expo Router GitHub Repository](https://github.com/expo/router)
- [Expo Router Installation Guide](https://docs.expo.dev/router/install/)

## Estructura Final Recomendada

```
home/
├── _layout.tsx (Stack principal único)
├── tasks/
│   ├── index.tsx
│   └── [id]/
│       └── index.tsx
├── treatments/
│   ├── index.tsx
│   └── [id]/
│       └── index.tsx
└── health-records/
    ├── index.tsx
    └── [id]/
        └── index.tsx
```

## Lecciones Aprendidas

1. **Comprender la jerarquía de stacks**: Cada `<Stack>` crea un contexto de navegación independiente
2. **Planificar la estructura de navegación**: Diseñar la estructura de rutas antes de implementar
3. **Usar el stack nativo**: Confiar en el comportamiento nativo de Expo Router para botones de retroceso
4. **Navegar con rutas relativas**: Usar rutas relativas al stack actual para mantener el historial
5. **Documentar decisiones de arquitectura**: Registrar por qué se toman ciertas decisiones de navegación

## Próximos Pasos

- [ ] Probar navegación desde notificaciones push
- [ ] Verificar comportamiento en diferentes dispositivos
- [ ] Documentar patrones de navegación para futuras funcionalidades
- [ ] Considerar implementar navegación modal para casos específicos

---

**Fecha de implementación**: [Fecha actual]  
**Branch**: [Nombre de la branch]  
**Desarrolladores**: [Nombres del equipo]
