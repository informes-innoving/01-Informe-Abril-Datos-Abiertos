# php-soda-MIN
## Adaptación de la librería php-soda al programa MIN-ALCALDÍA (Alcaldía de Pereira)
La biblioteca php-soda-MIN está diseñada para trabajar con los datos de MIN-ALCALDÍA, utilizando la API de datos abiertos de Socrata. Se proporciona como una alternativa a la implementación oficial de Socrata, esta biblioteca llena las deficiencias de la biblioteca oficial al proporcionar más funcionalidad, un enfoque más orientado a objetos, documentación y mucho código de ejemplo.

Esta biblioteca es totalmente compatible con la interacción con la API de datos abiertos de Socrata (SODA) mediante la obtención de conjuntos de datos, el manejo de tokens, el manejo de autenticación básica y tokens OAuth2.0 para escribir o modificar conjuntos de datos.

# Requisitos
PHP 5.6+

# Instalación
Esta biblioteca está disponible en Packagist como allejo / php-soda, agréguela usando Composer.

Si no está disponible Composer, esta biblioteca también se proporciona como un archivo Phar para que la incluya en su código. Obtenga el último archivo de Phar de nuestros lanzamientos.

# Utilización básica
Aquí hay algunos ejemplos rápidos sobre cómo funciona php-soda-MIN, pero hay mucho más que se puede hacer.

# Obtener un dataset

// Se crea un cliente con información sobre la API para manejar tokens y autenticación
$sc = new SodaClient("opendata.socrata.com");

// Acceder a un dataset con base en el 'end point' del API
$ds = new SodaDataset($sc, "pkfj-5jsd");

// Crear un SoqlQuery que será utilizado para filtrar los resultados del dataset
$soql = new SoqlQuery();

// Escribir un SoqlQuery
$soql->select("date_posted", "state", "sample_type")
     ->where("state = 'AR'")
     ->limit(1);

// Buscar el dataset en un array asociativo
$results = $ds->getDataset($soql);

# Actualizando un dataset

// Cree un cliente con información sobre la API para manejar tokens y autenticación.
$sc = new SodaClient("opendata.socrata.com", "<token here>", "email@example.com", "password");

// El conjunto de datos para cargar
$data = file_get_contents("dataset.json");

// Acceda a un conjunto de datos basado en el punto final de la API
$ds = new SodaDataset($sc, "1234-abcd");

// Para actualizar un conjunto de datos
$ds->upsert($data);

// 
Para reemplazar un conjunto de datos
$ds->replace($data);

Nota: Esta biblioteca admite la escritura directamente en conjuntos de datos con la API de datos abiertos de Socrata. Para conjuntos de datos con una o más transformaciones de datos aplicadas al esquema a través de Socrata Data Management Experience (la interfaz de usuario para crear conjuntos de datos), use la API de Socrata Data Management para aplicar esas mismas transformaciones a todas las actualizaciones. Para obtener más detalles sobre cuándo usar SODA frente a la API de administración de datos de Socrata, consulte la documentación de la API de administración de datos.

# Ayuda
Secretaría TIC de la Alcaldia de Pereira. Para informar un error o solicitar una función, envíe un mensaje por SAIA.

# IRC
Channel: #socrata-soda

Network: irc.freenode.net

# Gracias a...
Librería Oficial de Socrata PHP

Librería de C# Socrata

# Licencia
MIT
