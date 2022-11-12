---
title: "Una nueva fuente para avances en la actualización cartográfica"
date: 2022-11-12
tags: 
- censo
- bolivia
---

El 8 de noviembre el [Instituto Nacional de Estadística](https://www.ine.gob.bo/) (INE) publicó una capa geográfica con datos del avance en la actualización cartográfica a nivel municipal. En particular nos dice cuántas áreas de trabajo están planificadas y cuántas ya se han concluido o están en proceso. La división entre estos dos valores es el *porcentaje de avance* que el INE comunica en sus reportes orales. Los datos en esta capa son coherentes con información en notas de prensa recientes.

**Podemos distinguir entre áreas en proceso y áreas concluidas?** No, lo cual es casualmente conveniente para que el INE infle cómo se percibe su avance. Pero no debería ser muy importante, el INE suele concentrar sus brigadas en pocos lugares y un área de trabajo debería concluirse en un par de semanas. No he realizado el ejercicio pero es posible calcular el número medio de días que el INE toma en una área en base a los datos que capturé entre mediados de agosto y fines de septiembre. Por ejemplo, [éstos](https://github.com/mauforonda/canceles_elevando/commits/8d16738be2f12b4aee758f0efd135c98327ef1cb/data/cartografia/departamentos/beni.csv?browsing_rename_history=true&new_path=data/cartografia/old/departamentos/beni.csv&original_branch=master) son los cambios diarios a registros en áreas de Beni. 

**El INE actualiza estos datos?** No sé, pero tengo mucha curiosidad así que ya escribí [código](https://github.com/mauforonda/canceles_elevando/blob/4cdd650665e06c8306eca34e351ee69a0115dcf3/update/areas_cartografia.py) para consultar la fuente [cada media noche](https://github.com/mauforonda/canceles_elevando/blob/4cdd650665e06c8306eca34e351ee69a0115dcf3/.github/workflows/update.yml#L4) y construir una [serie diaria](https://github.com/mauforonda/canceles_elevando/blob/master/data/cartografia/areas_concluidas_o_en_proceso.csv). La fecha en esta serie hace referencia al día que termina. 

Una sorpresa agradable es que estos datos incluyen el código de cada municipio, lo cual no es común y facilita combinarlos con otras tablas. La aplicación más obvia es construir un mapa, así que ya hice un [cuaderno en observable](https://observablehq.com/d/76647fe240cadd76) que consume estos datos y los muestra geográficamente. En caso que el INE actualice estos datos, podría programar al menos una vista a la serie de tiempos y una proyección super simple de cuándo debería terminar con todas las áreas en el país.

![[images/Pasted image 20221112104928.png]]

**Cómo encontré estos datos?** No podía dormir así que me puse a revisar novedades recientes en mi [registro diario de servidores geográficos](https://github.com/mauforonda/geodatos/). Estos datos aparecieron por primera vez [en la madrugada del 9 de noviembre](https://github.com/mauforonda/geodatos/commit/cd567cf18a7ac6f92f527a7a31ca144bb9e250d7#diff-cb0da279bda65c03ccd31ff71d5dc8b79a9cb0651527903bdf836880fa2f493bR2796). Obviamente, sólo viendo el nombre `seguimiento:vw_ac_2021_cartografia` nadie podría saber de qué trata así que consulto ese nombre en mi [visor de mapas](https://observablehq.com/@mauforonda/datos-geograficos-del-gobierno-boliviano) y voilà! veo un mapa similar al que terminé reproduciendo. Las pistas principales eran que el servicio donde se subieron los datos pertenece al INE (SIGED) y el nombre de la capa incluye `ac`. Al INE le encanta nombrar artefactos en su infraestructura con acrónimos de los proyectos a los que están dedicados, por ejemplo `eh` para Encuesta de Hogares o `ac` para Actualización Cartográfica. 

No espero realmente retomar el monitoreo que hacía del [proyecto](https://observablehq.com/@mauforonda/avance-del-censo) [censal](https://observablehq.com/@mauforonda/nuevo-avance-del-censo). Se ha vuelto un tema demasiado delicado y la poca información disponible no sólo no ayuda a resolver ningún tema en debate, sino que podría ser prestada como instrumento para la violencia de uno u otro lado. Capturo estos datos porque, si son actualizados regularmente, el costo de oportunidad de no construir una serie de tiempos, aunque su valor sea incierto, me parece importante. Y creo el cuaderno y el mapa porque son el medio más cómodo para observar esta información.

Veamos 🥱