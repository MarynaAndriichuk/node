# Seguridad

## Reportando un error en Node.js

Informar de errores de seguridad en Node.js a través de [HackerOne](https://hackerone.com/nodejs).

Su informe será reconocido en 24 horas, y recibirá una respuesta más detallada a su informe en 48 horas indicando los siguientes pasos en el manejo de su envío.

Después de la respuesta inicial a su informe, el equipo de seguridad se esforzará por mantenerle informado del progreso realizado hacia un anuncio completo y reparador, y puede solicitar información adicional o orientación sobre el asunto reportado.

### Programa de recompensas de errores Node.js

El proyecto Node.js participa en un programa oficial de recompensas de errores para investigadores de seguridad y divulgaciones públicas responsables.  El programa se gestiona a través de la plataforma HackerOne. Vea <https://hackerone.com/nodejs> para más detalles.

## Reportando un error en un módulo de terceros

Los errores de seguridad en los módulos de terceros deben ser reportados a sus respectivos mantenedores y también deben ser coordinados a través del Node. s Equipo de Seguridad Ecosystem a través de [HackerOne](https://hackerone.com/nodejs-ecosystem).

Los detalles de este proceso se pueden encontrar en el repositorio de [Grupo de Trabajo de Seguridad](https://github.com/nodejs/security-wg/blob/HEAD/processes/third_party_vuln_process.md).

Gracias por mejorar la seguridad de Node.js y su ecosistema. Sus esfuerzos y su divulgación responsable son muy apreciados y serán reconocidos.

## Política de divulgación

Aquí está la política de divulgación de seguridad para Node.js

* Se recibe el informe de seguridad y se le asigna un manejador principal. Esta persona coordinará el proceso de reparación y liberación. El problema está confirmado y se determina una lista de todas las versiones afectadas. El código se audita para encontrar posibles problemas similares. Las correcciones se preparan para todas las versiones que todavía están en mantenimiento. Estas correcciones no están comprometidas con el repositorio público, sino que se mantienen localmente en espera del anuncio.

* Se ha elegido una fecha de embargo sugerida para esta vulnerabilidad y se ha solicitado un CVE (Vulnerabilidades y Exposiciones Comunes (CVE®)) para la vulnerabilidad.

* En la fecha del embargo se envía una copia del anuncio a la lista de correo de seguridad de Node.js. Los cambios se insertan en el repositorio público y se implementan nuevas compilaciones en nodejs.org. En el plazo de 6 horas desde que se notificara la lista de correo, se publicará una copia del aviso en el blog de Node.js.

* Normalmente, la fecha del embargo se fijará 72 horas a partir de la fecha de emisión del CVE. Sin embargo, esto puede variar dependiendo de la gravedad del error o dificultad en la aplicación de una solución.

* Este proceso puede tomar algún tiempo, especialmente cuando se requiere coordinación con los mantenedores de otros proyectos. Se hará todo lo posible para manejar el error de la manera más oportuna posible; sin embargo, es importante que sigamos el proceso de liberación anterior para asegurar que la divulgación se maneja de forma consistente.

## Recibiendo actualizaciones de seguridad

Las notificaciones de seguridad se distribuirán a través de los siguientes métodos.

* [https://groups.google.com/group/nodejs-seg](https://groups.google.com/group/nodejs-sec)
* [https://nodejs.org/es/blog/](https://nodejs.org/en/blog/)

## Comentarios sobre esta política

Si tiene sugerencias sobre cómo se podría mejorar este proceso, por favor envíe un [pull request](https://github.com/nodejs/nodejs.org) o [archivo un problema](https://github.com/nodejs/security-wg/issues/new) para discutir.
