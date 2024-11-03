# Disseny-DDBB
![DDBB](https://github.com/user-attachments/assets/0a0bc377-baf7-4a43-af3c-9d30daa9bacb)
# Diseño de Base de Datos para el Festival de Música

Este proyecto contiene el diseño de una base de datos para gestionar un festival de música, siguiendo los requisitos especificados por el ayuntamiento.

## Entidades y Atributos

### Recinte (Recinto)
- **Identificador**: `nom` (Nombre del recinto, ej. "Sonar Hall")
- `metres_quadrats_escenari` (Metros cuadrados del escenario)
- `metres_quadrats_zona_espectadors` (Metros cuadrados de la zona de espectadores)
- `aforament_maxim` (Aforo máximo)
- `lavabos` (Booleano: dispone o no de lavabos)
- `escenari_cobert` (Booleano: el escenario está cubierto o no)

### Grup (Grupo musical)
- **Identificador**: `nom` (Nombre del grupo)
- `pais` (País de origen del grupo)
- `nombre_components` (Número de componentes de la banda)
- `preu_per_concert` (Precio por cada concierto)

### Concert (Concierto)
- **Identificador**: `id_concert`
- `grup` (FK de "Grup")
- `recinte` (FK de "Recinte")
- `dia` (Fecha del concierto)
- `hora_inici` (Hora de inicio)
- `hora_final` (Hora de fin)

### Substitut (Grupo sustituto)
- `grup_substituit` (FK de "Grup")
- `grup_substitut` (FK de "Grup")

### Carrer (Calle en la zona de acampada)
- **Identificador**: `codi` (Código de la calle)
- `nom` (Nombre del grupo musical famoso asociado a la calle)

### Parcel·la (Parcela en la zona de acampada)
- **Identificador**: `numero_parcela` (Identificador único por calle)
- `carrer` (FK de "Carrer")
- `extensio_metres_quadrats` (Extensión en metros cuadrados)
- `preu` (Precio de la parcela)

### Assistents (Asistentes al festival)
- **Identificador**: `usuari` (Usuario único)
- `contrasenya` (Contraseña)
- `dni_o_passaport`
- `mail`
- `dades_personals` (Datos personales adicionales)

### Lloguer (Alquiler de parcela)
- **Identificador**: `id_lloguer`
- `responsable` (FK de "Assistents", responsable del alquiler)
- `parcela` (FK de "Parcel·la")

### Accés (Acceso de asistentes a los recintos)
- **Identificador**: `id_acces`
- `assistents` (FK de "Assistents")
- `recinte` (FK de "Recinte")
- `hora_acces` (Hora de acceso)

## Relaciones

1. **Grup - Concert**: Un grupo puede participar en múltiples conciertos en distintos recintos y fechas. Relación uno a muchos.
2. **Recinte - Concert**: Cada recinto tiene varios conciertos. Relación uno a muchos.
3. **Grup - Substitut**: Un grupo puede tener uno o varios sustitutos y un grupo puede ser sustituto de varios otros. Relación de muchos a muchos.
4. **Carrer - Parcel·la**: Cada calle tiene múltiples parcelas. Relación uno a muchos.
5. **Assistents - Lloguer - Parcel·la**: Cada asistente puede alquilar solo una parcela, y una parcela solo tiene un responsable. Relación uno a uno entre "Assistents" y "Lloguer", y uno a muchos entre "Lloguer" y "Parcel·la".
6. **Assistents - Accés - Recinte**: Los asistentes pueden acceder libremente a todos los recintos, por lo que es una relación de muchos a muchos que se gestiona en la tabla "Accés".

