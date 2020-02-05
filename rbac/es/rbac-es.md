# Guía administrativa: El control de acceso basado en roles

El control de acceso en CloudMC se alcanza a través un modelo flexible y multi-occupante, que provee una manera simplificada de gestionar los permisos por todas partes du una jerarquía de organizaciones y entornos.  La funcionalidad del control de acceso basado en roles que viene con CloudMC permite un control preciso de los permisos que son otorgados a los usuarios.

## Definiciones
- **Permiso:** Una autorización para ejecutar alguna tarea.  **Permisos del sistema** rigen el acceso a la funcionalidad en la consola de CloudMC, **permisos entornales** rigen el acceso a los recursos de un servicio

- **Rol de sistema:**  Una colección compuesta de permisos de sistema, dentro de una organización.  CloudMC viene con **roles fijados** que no pueden ser modificados, y **roles personalizados** pueden ser creados.  Generalmente, los roles de sistema se refieren simplemente como ≪roles≫

- **Alcance:** La organización o organizaciones a cual un rol de sistem se aplica

- **Organización:** Una agrupación de usuarios relacionados.  Una instalación base de CloudMC ya viene con la organización **System**

- **Usuario:** Una cuenta usuaria es la manera que un individuo se connecta al portal de CloudMC.  Un usuario siempre está asignado un rol de sistema primario en la organización donde se creó la cuenta.  Un usuario puede ser asignado roles de sistema adicionales, y que pueden ser recorridos a una o más organizaciones

- **Entorno:** Una unidad lógica dentro de una organización, usada para apartar y agrupar recusos de una manera segura.  El acceso está controlar por una combinación de roles entornales y de controles de acceso del alcance

- **Rol entornal:** Una colección compuesta de permisos entornales, que está asignada a los miembros de un entorno

![user access control chart](roles_chart-es.png)

## Los roles de sistema
La función del rol de sistema es a controlar el acceso a la funcionalidad de CloudMC en una manera sencilla y estandardizada.  Un rol de sistema puede ser asignado a usuarios dentro de una organización, además que permitir la colaboración a travès de las organizaciónes.  Los roles de sistema se rigen en el interfaz Web así como en el API de CloudMC.  Los roles personalizados pueden ser definidos con permisos que son alineados con las reglas del negocio.

Cada uno de los roles de sistema tiene un *alcance*, que puede ser uno de los siguientes:

- Todas las organizaciones
- Solamente las organizaciones de nivel superior
- Una organización específica sin sus sub-organizaciones
- Una organización específica con todos sus sub-organizaciones
- Solamente las sub-organizaciones de una organización específica
- Todas la organizaciones con una etiqueta específica

Usando la funcionalidad de etiquetas, el alcance de un rol asignado puede crecer automaticamente cuando una organización recibe la etiqueta, y se peuede reducir cuando la etiqueta se borra.  Esto permite escenarios donde el alcance del rol puede cambiarse en una manera dinámica basado en las reglas del negocio.

## Los roles fijados
Los roles fijados incorporados en CloudMC son applicables a una amplia gama de casos de uso.  Ellos pueden se asignados al rol primario de un usuario, o como un rol addicional.

Un sumario de cada rol fijado cuando aplicado como un rol primario:
- **Invitado:**  Un rol de solo-lectura.  Puede ver los recursos en los entornos los cuales la cuenta es miembro
- **Usuario:**  Puede crear nuevos entornos con conexiones de servicio que ya existen, y gestionar esos entornos los cuales es dueño
- **Administrador:**  Puede gestionar la organización.  Puede gestionar todos los entoronos en todas las conexiones de servico.  No tiene derecho ni de ver las sub-organizaciones ni de crear nuevas sub-organizaciones
- **Revendedor:**  Puede gestionar la imagen de marca y las tarificaciones de la organización y sus sub-organizaciones, y puede crear sub-organizaciones en la organización.  No puede crear nuevas organizaciones
- **Operador:**  Puede crear organizaciones y sub-organizaciones, gestionar conexiones de servicio, cuotas de servicio, compromisos, y tiene acceso completo a todas otras organizaciones, recursos y parámetros del sistema

Cada rol fijado tiene un alcance predeterminado:
- Invitado, Usuario, y Administrador:  Solamenta la organización dentro de que existe la cuenta usuaria
- Revendedor:  La organización dentro de que existe la cuenta usuaria, y todas sus sub-organizaciones
- Operador:  Todas las organizaciones

Como india el diagrama abajo, subiendo por la jerarquía cada rol tiene todos los privilegios que los precedents:

![permissions chart](permissions-en.png)

### Los roles personalizados

#### Crear un rol personalizado

## Los roles entornales

## Cómo asignar los roles
