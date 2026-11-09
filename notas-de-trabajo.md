# NOTAS DE TRABAJO
## Parte 1 · Adquisición en vivo
Con la máquina encendida, sigue el orden de volatilidad y anota en tus notas de trabajo la hora de cada paso, qué herramienta usas y por qué. No hagas instantáneas de la máquina en VirtualBox: lo que cambiara después se guardaría en otro fichero, fuera del .vmdk, y no llegaría a tu imagen.

### Fecha de la adquisición: 02/22/2026

```
NOTA: Durante toda la adquisición en vivo se ejcutan las herramientas por terminal, ya que al intentar abrirlas manualmente con la interfaz no se abrían o daban algunos errores.
```

#### Arranque de la máquina: 19:30
No hay desfase entre la hora de la máquina, y la hora real.

#### Creación archivos de marca: 19:31
Se crea un txt con nombre *marca-JuditQuiros.txt*, y se escribe en una nota (sin guardar) el texto: *AFI-JuditQuiros-20261102*

[Imagen del estado inicial de la máquina](./capturas/Estado-inicial-maquina.png)

#### Adquisición de la memoria ram: 
    - **Hora:** 19:45
    - **Herramienta:** winpmem_mini_x64_rc2.exe 
    - **Justificación herramienta:** DumpIt no era compatible con la versión de Windows 7 de la máquina a analizar, así que se usó esa version de winpmem que si lo era.
    - **Resultado:** memoria-ram.raw
    - **Notas:** En la herramienta sale que la hora del sistema lleva un desfase de 1h respecto a la hora real de ejecución de la misma.

[Imagen de la capturación de la ram](./capturas/memoria-ram-winPmem.png)

#### Datos Volátiles:
    - **Hora:** 19:55
    - **Herramienta:** Script propio modificado para que fuera compatible con el Windows 7 llamado *respuesta-en-vivo.ps1*
    - **Justificación herramienta:** He usado este script para obtener los datos volátiles que pudiera necesitar por si algo ha salido mal con la adquisición de la memoria ram.
    - **Resultado:** Carpeta generada con los archivos necesarios.

[Imagen captura de datos volátiles](./capturas/respuesta-en-vivo.png)

#### Triaje:
    - **Hora:** 20:00
    - **Herramienta:** velociraptor-v0.6.9-windows-amd64.exe
    - **Justificación herramienta:** Usé esta herramienta porque kape no funcionaba en la máquina, y esta versión de velociraptor si.
    - **Resultado:** triaje.raw

[Imagen captura del triaje](./capturas/triaje-velociraptor.png)

#### Tráfico de Red: 
    - **Hora:** 20:01 - 20:03
    - **Herramienta:** Terminal de Windows (PowerShell) 
    - **Justificación herramienta:** Se ha utilizado esos comandos siguiendo los pasos indicados por el profesor.
    - **Resultado:** No se creó ningún archivo tras pararlo, así que es probable que hiciera algo mal.
    - **Nota:** Los ejecuté después de hacer el triaje porque se me olvidó hacerlo antes.

[Imagen inicio de captura de red](./capturas/Inicio-captura-red.png)

[Imagen fin de la captura de red](./capturas/Fin-captura-red.png)

#### Comprobación de cifrado:
    - **Hora:** 20:04
    - **Herramienta:** EDD
    - **Justificación herramienta:** Esta permite comprobar si hay algún tipo de cifrado con BitLocker o con cualquier otra herraimenta de cifrado.
    - **Resultado:** No hay ningún disco cifrado, se puede apagar la máquina.

[Imagen comprobación del cifrado](./capturas/cifrado-EDD.png)

#### Apagado de la máquina: 20:13
Se apaga la máquina virual mediante el botón de VirtualBox que pone "Apagar la máquina"

[Imagen apagado de la máquina](./capturas/Apagado.png)

---

## Parte 2 · Adquisición post-mortem

### Fecha de la adquisición: 03/11/2026

#### El disco de la máquina

**Carpeta donde se encuentra el disco:** C:\Users\usuario\VirtualBox VMs\FORENSIC_10-7

**Nombre del disco (sólo hay uno):** FORENSIC_10_disk0.vdi

** Hash inicial del disco: **
- SHA256 -> 0AB0B4A393DBF303F51544906B03EF6841511EAD9349EA6C8AA93A7B5990F294
- MD5 -> c1c3493745b64e1d27b88983461c3504
- SHA1 -> 3f6e1e0458b46e586badd739c77f24b4c112606b

**Hash final:  (Igual)**
- SHA256 -> 0AB0B4A393DBF303F51544906B03EF6841511EAD9349EA6C8AA93A7B5990F294
- MD5 -> c1c3493745b64e1d27b88983461c3504
- SHA1 -> 3f6e1e0458b46e586badd739c77f24b4c112606b

[Imagen estado inicial del disco virtual](./capturas/estado-inicial-disco-virtual.png)

**Hash inicial de otros archivos:** (Comprobado antes y después y coinciden)
- Logs: 
    - VBox.log: AF343CE6F6CAE10F0DFF2F352E159510EC035C424C058DBC1E805D71F29C7571 (SHA256)
    - VBox.log.1: 2BC326D71517F4187866E7394D19FD11A78A51388517AD84B1F84A02F282B290 (SHA256)
    - VBox.log.2: FF77D84E0D7F3B753DAE0AA8B06D141CD94749298A70E3C5D3AE0A719D599128 (SHA256)
    - VBox.log.3: 4F4CBE43572B91A8C52CDF4BE9A2D98F96482315CD861422060722D7D4D92343 (SHA256)
    - VBoxHardening.log: 5937C97EC2C09DED72E5A4EF3296A6DF96C04BC06881D41D84E06DCABE984A70 (SHA256)
    
- FORENSIC_10-7.vbox: 2567A1BFCE9E97314B8A04A185E57FAF32F91D5236F05779A2E83D31544301F9 (SHA256) 

- FORENSIC_10-7.vbox-prev:  36A2CA7787E7F9D50E572987C85F0820848F64165A8FF962C294B4645DAB338C (SHA256)

**Herramienta usada para hacer la imagen:** FTK imager 8.3.0.27

[Imagen de captura del disco virtual](./capturas/Imagen-disco-virtual.png)

---

#### El pendrive encontrado

[Imagen inicial del pendrive](./capturas/bloqueadora-escritura.jpeg)

**Herramienta de bloqueo:** Tableau Forensic USB 3.0 Bridge (T8u).

**Herramienta para hacer la imagen de disco:** FTK Imager 8.3.0.27

[Imagen de captura del Pendrive](./capturas/Imagen-fisica-pen.png)

---

## Parte 3 · Busca tu marca

**En windows** me sale la marca en la RAM pero no me sale en el triaje.

- [Marca en la RAM en Windows](./capturas/buscar-marca-windows1.png)

- [Marca en el triaje en Windows](./capturas/buscar-marca-windows2.png)

**En ubuntu** no me sale ninguna marca: [Marca de la RAM y Triaje en Ubuntu](./capturas/buscar-marca-ubuntu.png)


## Parte 4 · Cadena de custodia

[Enlace al acta de la adquisición.pdf](acta-adquisicion.pdf)

[Enlace al registro de la cadena de custodia.pdf](registro-cadena-custodia.pdf)