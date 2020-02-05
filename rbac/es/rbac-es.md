# Guía administrativa: El control de acceso basado en roles

El control de acceso en CloudMC se alcanza a través un modelo flexible y multi-occupante, que provee una manera simplificada de gestionar los permisos por todas partes du una jerarquía de organizaciones y entornos.  La funcionalidad del control de acceso basado en roles que viene con CloudMC permite un control preciso de los permisos que son otorgados a los usuarios.

## Definiciones
- **Permiso:** Un autorización para ejecutar alguna tarea.  **Permisos del sistema** rigen el acceso a la funcionalidad en la consola de CloudMC, **permisos entornales** rigen el acceso a los recursos de un servicio

- **Rol de sistema:**  Una colección compuesta de permisos de sistema, dentro de una organización.  CloudMC viene con **roles fijados** que no pueden ser modificados, y **roles customizados** pueden ser creados.  Generalmente, los roles de sistema se refieren simplemente como ≪roles≫

- **Ámbito:** La organización o organizaciones a cual un rol de sistem se aplica

- **Organización:** Una agrupación de usuarios relacionados.  Una instalación base de CloudMC ya viene con la organización **System**

- **Usuario:** Una cuenta usuaria es la manera que un individuo se connecta al portal de CloudMC.  Un usuario siempre está asignado un rol de sistema primario en la organización donde se creó la cuenta.  Un usuario puede ser asignado roles de sistema adicionales, y que pueden ser recorridos a una o más organizaciones

- **Entorno:** Una unidad lógica dentro de una organización, usada para apartar y agrupar recusos de una manera segura.  El acceso está controlar por una combinación de roles entornales y de controles de acceso del ámbito

- **Rol entornal:** Una colección compuesta de permisos entornales, que está asignada a los miembros de un entorno


![user access control chart](roles_chart-es.png)

## Los roles de sistema

## Los roles fijados
solo-lectura

### Los roles customizados

#### Crear un rol customizado

## Los roles entornales

## Cómo asignar los roles
