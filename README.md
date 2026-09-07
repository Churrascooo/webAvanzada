# webAvanzada
Lab 1 OII-436-1
Ariel Carrasco Suárez - 21.754.057-7
Gabriel Reyes - 21.629.868-3

Pregunta 1: ¿Por qué no se recomienda desarrollar directamente sobre main en este laboratorio?
R: No se recomienda desarrollar sobre el main porque esta rama debe contener cambios testeados y verificados. Con esto nos referimos a que deben ser una actualización final, en donde todo lo que sea desarrollo y pruebas debe ser en otra rama, en este caso devops/ci-cd.

Pregunta 2: ¿Qué problema se evita al utilizar --skip-git al crear el proyecto Angular?
R: Porque el repositorio ya está creado. Sin el --skip se crearía un segundo repositorio.

Pregunta 3: ¿Qué verifica npm run build en esta etapa del laboratorio?
R: Verifica que se cree correctamente el frontend y se pueda ejecutar y conectar con el localhost.

Pregunta 4: ¿Qué utilidad tiene revisar git status o git diff --cached antes de realizar un commit?
R: Permite ver las diferencias entre el antes y después de hacer algún cambio en el código antes de enviar el commit.

Pregunta 5: ¿Qué evento activa el workflow ci.yml?
R: Lo activa el pull request, eso se puede ver en esta linea dentro del workflow:
on:
  pull_request:
    branches: [main]

Pregunta 6: En runs-on: ubuntu-latest, ¿qué representa ubuntu-latest?
R: Representa que el runner debe utilizar la versión más actualizada de ubuntu.

Pregunta 7: Ordene las etapas de validación que ejecuta el job frontend y explique por qué npm ci se ejecuta
antes que las pruebas.
R: El orden es:
 	- name: Obtener código
 	- name: Configurar Node.js
 	- name: Instalar dependencias
 	- name: Ejecutar pruebas
 	- name: Construir Angular

	npm ci debe ejecutarse antes de las pruebas porque este comando instala las dependencias necesarias para posteriormente construir Angular, no se podría invertir el orden.

Pregunta 8: Después del push, indique qué etapa del pipeline falla y qué ocurre con las etapas siguientes.
R: En la etapa de pruebas, especificamente en esta parte del workflow se detalla:
App debe mostrar el título del catálogo FAILED
	Expected 'Catálogo de Recursos' to contain 'Título incorrecto'.

Dado este fallo, los siguientes que dependían del mismo no pudieron completarse (Construir Angular y Post Configurar Node.js).

Pregunta 9: ¿Debería integrarse este Pull Request a main mientras el pipeline está fallando? Justifique
R: No, ya que a main debe ir solamente cambios que se ejecuten correctamente. Esta es la ventaja de trabajar con una branch(es).

Pregunta 10: Clasifique cada elemento como “versionable”, “variable/configuración” o “secreto/no
versionable”: package.json, API_URL pública, AWS_REGION, DB_PASSWORD, API_TOKEN, terraform.tfstate.
R: package.json = versionable
   API_URL_pública = variable/configuración
   AWS_REGION = variable/configuración
   DB_PASSWORD = secreto/no versionable
   API_TOKEN = secreto/no versionable
   terraform.tfstate = secreto/no versionable

Pregunta 11: ¿Por qué una contraseña o token no debe escribirse directamente dentro de ci.yml, cd.yml o un
archivo TypeScript del frontend?
R: Porque quedaría expuesto a cualquiera que acceda al repositorio.

Pregunta 12: Si un secreto real fue incluido en un commit y luego se agrega su archivo a .gitignore, ¿queda
solucionado el problema? Explique qué acción adicional debe realizarse.
R: No, porque igualmente queda en el historial de github. Lo que se podría hacer es eliminar el archivo del historial.

Pregunta 13: ¿Qué diferencia existe entre terraform validate, terraform plan y terraform apply?
R: validate verifica que la configuración sea valida, plan son las acciones que realizará y apply es ejecutar las acciones de plan.

Pregunta 14: ¿Por qué ci.yml se activa con pull_request y cd.yml se activa con push sobre main?
R: Por cómo están configurados los workflows 
cd: 
  on:
    push:
     branches: [main]

ci: 
  on:
    pull_request:
     branches: [main]

Pregunta 15: ¿Qué función cumple Terraform dentro de este flujo de CD?
R: Sirve para gestionar la infraestructura como código, en el flujo de CD permite la automatización.

Pregunta 16: ¿Por qué el workflow usa ${{ secrets.DEMO_TOKEN }} en lugar de escribir el valor directamente?
R: Para mantener el valor oculto, si estuviera directamente quedaría expuesto a cualquiera.