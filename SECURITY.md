# Guía de Seguridad - Maxicupones CRM

## Overview

Esta guía documenta las medidas de seguridad implementadas para proteger las credenciales y configuraciones sensibles del proyecto.

## Problemas de Seguridad Corregidos

### 1. Exposición de Credenciales Firebase
- **Problema**: Credenciales Firebase hardcodeadas en archivos TypeScript
- **Solución**: Implementación de variables de entorno con `process.env`
- **Archivos modificados**: `src/environments/environment.ts`, `src/environments/environment.prod.ts`

### 2. Archivos .env en Control de Versiones
- **Problema**: No existían archivos .env y el .gitignore no los excluía
- **Solución**: Creación de archivos `.env.example` y actualización de `.gitignore`

### 3. Falta de Herramientas de Seguridad
- **Problema**: No existían scripts para verificación de seguridad
- **Solución**: Scripts automatizados para configuración y verificación

## Configuración Rápida

### Paso 1: Configurar Variables de Entorno

```bash
# Para desarrollo
npm run setup:env:dev

# Para producción
npm run setup:env:prod
```

### Paso 2: Editar Archivos .env

Edita los archivos creados con tus credenciales reales:

```bash
# Desarrollo
code .env.local

# Producción
code .env.production
```

### Paso 3: Verificar Seguridad

```bash
npm run security:check
```

## Variables de Entorno Requeridas

### Firebase Configuration
- `FIREBASE_API_KEY`: API key de Firebase
- `FIREBASE_AUTH_DOMAIN`: Dominio de autenticación
- `FIREBASE_DATABASE_URL`: URL de base de datos
- `FIREBASE_PROJECT_ID`: ID del proyecto
- `FIREBASE_STORAGE_BUCKET`: Bucket de almacenamiento
- `FIREBASE_MESSAGING_SENDER_ID`: Sender ID para messaging
- `FIREBASE_APP_ID`: ID de la aplicación
- `FIREBASE_MEASUREMENT_ID`: ID de Analytics (opcional)

## Archivos de Configuración

### Archivos Seguros (Versionados)
- `.env.example` - Plantilla para desarrollo
- `.env.production.example` - Plantilla para producción
- `src/environments/environment.ts` - Usa variables de entorno
- `src/environments/environment.prod.ts` - Usa variables de entorno

### Archivos Excluidos (No Versionados)
- `.env.local` - Credenciales de desarrollo
- `.env.production` - Credenciales de producción
- `environment.local.ts` - Configuración local adicional

## Scripts de Seguridad

### setup-env.js
Automatiza la creación de archivos .env desde las plantillas.

```bash
node scripts/setup-env.js [development|production]
```

### security-check.js
Verifica la seguridad de las credenciales y configuración.

```bash
node scripts/security-check.js
```

## Mejores Prácticas

### 1. Rotación de Credenciales
- Genera nuevas API keys en Firebase Console
- Revoca las credenciales anteriores expuestas
- Actualiza los archivos .env con las nuevas credenciales

### 2. Separación de Ambientes
- Usa diferentes proyectos Firebase para desarrollo y producción
- Mantén credenciales completamente separadas
- Implementa diferentes niveles de permisos

### 3. Control de Acceso
- Limita el acceso a archivos .env al equipo necesario
- Usa gestores de secretos en producción (Firebase Hosting, Vercel, etc.)
- Implementa revisión de código para cambios de configuración

### 4. Monitoreo
- Ejecuta `npm run security:check` regularmente
- Configura alertas para cambios en credenciales
- Revisa los logs de Firebase por acceso no autorizado

## Comandos Útiles

```bash
# Configuración inicial
npm run setup:env:dev
npm run setup:env:prod

# Verificación de seguridad
npm run security:check

# Desarrollo
npm start

# Build producción
npm run build

# Deploy
npm run deploy
```

## Acciones Inmediatas Requeridas

1. **ROTAR CREDENCIALES**: Las credenciales anteriores están expuestas en el historial de Git
2. **CONFIGURAR .env**: Crea los archivos .env con nuevas credenciales
3. **VERIFICAR SEGURIDAD**: Ejecuta el script de verificación
4. **ACTUALIZAR EQUIPO**: Comunicar los cambios al equipo de desarrollo

## Soporte

Para cualquier duda sobre la configuración de seguridad:
1. Ejecuta `npm run security:check` para diagnóstico
2. Revisa esta guía para solución de problemas
3. Contacta al equipo de seguridad para casos críticos

---

**Importante**: Esta guía debe ser mantenida actualizada con cualquier cambio en la configuración de seguridad del proyecto.
