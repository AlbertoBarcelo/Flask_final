# Flask_Birthdays


Lo primero que hemos de hacer es descargar el archivo.zip que nos proporciona el tutorial, cuando lo tenemos descargado hemos de crear un proyecto al que lo podamos añadir.

Ahora lo que haremos sera ir analiando poco a poco los diferentes archivos que forman parte de nuestra aplicación.

-------
## APP.PY

En este punto lo que se busca es configurar la conexión con la base de datos
``` ruby
db = SQL("sqlite:///birthdays.db")
```
Definimos el metodo POST
``` ruby
 if request.method == "POST":
        message = ""
        name = request.form.get("name")
        month = request.form.get("month")
        day = request.form.get("day")
        db.execute(
             "INSERT INTO birthdays (name, month, day) VALUES(?, ?,?)",
             name,
             month,
             day,
         )
        birthdays = db.execute("SELECT * FROM birthdays")
        return render_template("index.html", message=message, birthdays=birthdays)
```
En este punto podemos ver como adquirimos los datos y los guradamos en variables para poder utilizarlos a continuación, como podemos ver estamos declarando las sigientes variables, ya que como queremos saber el nombre, el mes y el dia de cumpleaños pues por ello mismo estas son las variables que hemos declarado.
``` ruby
   name = request.form.get("name")
   month = request.form.get("month")
   day = request.form.get("day")
```

Aquí podemos ver como se estrucuran los datos que mandaremos a nuestra base de datos, como se puede observar insertaremos el nombre, el mes y el dia de cumpleaños.
``` ruby
db.execute(
    "INSERT INTO birthdays (name, month, day) VALUES(?, ?,?)",
     name,
     month,
     day,
            )
```

En este ultimo punto podemos ver como se recuperan los datos de la base de datos para poder volver a mostrar los datos junto a los nuevos datos que le hemos añadido.
``` ruby
        birthdays = db.execute("SELECT * FROM birthdays")
        return render_template("index.html", message=message, birthdays=birthdays)
```
-------
## INDEX.HTML
``` ruby
<!DOCTYPE html>

<html lang="en">

<head>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@500display=swap" rel="stylesheet">
    <link href="/static/styles.css" rel="stylesheet">
    <title>Birthdays</title>
</head>

<body>
    <div class="jumbotron">
        <h1>Birthdays</h1>
    </div>
    <div class="container">
        <div class="section">
            <h2>Add a Birthday</h2>
            <form action="/" method="POST">
                <input name="name" type="text" placeholder="Name" autocomplete="off" autofocus>
                <input name="month" type="number" placeholder="Month" max="12" min="1" autocomplete="off" autofocus>
                <input name="day" type="number" placeholder="Day" max="31" min="1" autocomplete="off" autofocus>
                <input type="submit" value="Add Birthday">
            </form>
        </div>

        <div class="section">

            <h2>All Birthdays</h2>
            <table>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Birthday</th>
                    </tr>
                </thead>
                <tbody>
                    {% for birthday in birthdays %}
                    <tr>
                        <td>{{ birthday.name }}</td>
                        <td>{{ birthday.month}}/{{ birthday.day }}</td>
                    </tr>
                    {% endfor %}
                </tbody>
            </table>
        </div>
    </div>
</body>

</html>
```

Si seguimos el tutorial llegamos al paso en el que hemos de crear los input para poder añadir nuevos cumpleaños a nuestra aplicación, y esto es lo que hacemos en este momento, clo que hacemos es crear un input para cada cosa que queremos que el usario nos inserte, es decir uno para el nombre, otro para el mes y otro para el dia y para acabar crearemos un boton para enviar la información a nuestra base de datos.
``` ruby
     <input name="name" type="text" placeholder="Name" autocomplete="off" autofocus>
     <input name="month" type="number" placeholder="Month" max="12" min="1" autocomplete="off" autofocus>
     <input name="day" type="number" placeholder="Day" max="31" min="1" autocomplete="off" autofocus>
     <input type="submit" value="Add Birthday">
```

En este punto lo que hacemos es crear la tabla donde iremos mostrando todos los cumpleaños de forma ordenada, se mostrará en el siguiente orden, preimero el nombre a continuación el mes y por último el dia.
``` ruby
          <table>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Birthday</th>
                    </tr>
                </thead>
                <tbody>
                    {% for birthday in birthdays %}
                    <tr>
                        <td>{{ birthday.name }}</td>
                        <td>{{ birthday.month}}/{{ birthday.day }}</td>
                    </tr>
                    {% endfor %}
                </tbody>
            </table>
```
# Conclusión

Llegados a este paso ya hemos acabado el tutorial y lo que hemos de hacer ahora es descargar el entorno que tenemos en este mismo repositorio, dentro de el abriremos una terminal y ejecutaremos el siguinte comando **pip install cs50.
 
Una vez ya tenemos el entorno preparado ejecutaremos **flask --app app run** este comando sirve para iniciar nuestra aplicación una vez arranque mantendremos pulsado ctrl + click en la ruta que nos aparezca: 

![imagen](https://github.com/AlbertoBarcelo/Flask_final/assets/114684379/0964a475-8f2d-42e6-8c64-f6b917aff112)

Esperaremos un momento y se nos abrira en el navegador nuestra aplicació y ya podremos utilizarla.
![imagen](https://github.com/AlbertoBarcelo/Flask_final/assets/114684379/81445a0b-4f77-4486-871e-fc95514086c5)

Y para comprobarlo añadiremos un cumpleaños:
![imagen](https://github.com/AlbertoBarcelo/Flask_final/assets/114684379/47c01def-e552-434b-bafd-73dfde36012b)

Y como podemos ver al pulsar el boton que pone "Add Birthday" ya nos ha aparecido el nuevo cumpleaños en la tabla:
![imagen](https://github.com/AlbertoBarcelo/Flask_final/assets/114684379/f7996af8-0473-41bc-92c9-9b0cd27920ef)


