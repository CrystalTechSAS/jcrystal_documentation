### Configuración adicional para Angular2
Se debe crear el archivo de configuración en `src/util/app-configuration.ts` con el siguiente contenido
```typescript
export class AppConfiguration{
  static DEBUG = true;
}
```
#### Dependencias
El código generado para Typescript depende de estas librerías:
- [moment](https://www.npmjs.com/package/moment)
- [sweetalert](https://www.npmjs.com/package/sweetalert)
Adicionalmente se debe incluir la librería XXXXX en el modulo principal.