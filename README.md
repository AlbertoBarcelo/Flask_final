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
        if not name:
            message = "Missing name"
        elif not month:
            message = "Missing month"
        elif not day:
            message = "Missing day"
        else:
            db.execute(
                "INSERT INTO birthdays (name, month, day) VALUES(?, ?,?)",
                name,
                month,
                day,
            )
        birthdays = db.execute("SELECT * FROM birthdays")
        return render_template("index.html", message=message, birthdays=birthdays)
```
En este punto podemos ver como adquirimos los datos y los guradamos en variables para poder utilizarlos a continuación.
``` ruby
   name = request.form.get("name")
        month = request.form.get("month")
        day = request.form.get("day")
```

Aquí podemos ver como se actuara en el caso de que se de uno de los siguintes errores.
``` ruby
 if not name:
            message = "Missing name"
        elif not month:
            message = "Missing month"
        elif not day:
            message = "Missing day"
        else:
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
            <div class="error_message">
                {{ message }}
            </div>
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

Creamos un div donde colocaremos el mensaje de error en el momento que el usuario haga algo que no este disponible.
``` ruby
 <div class="error_message">
                {{ message }}
            </div>
```

Si seguimos el tutorial llegamos al paso en el que hemos de crear los input para poder añadir nuevos cumpleaños a nuestra aplicación, y esto es lo que hacemos en este momento
``` ruby
     <input name="name" type="text" placeholder="Name" autocomplete="off" autofocus>
     <input name="month" type="number" placeholder="Month" max="12" min="1" autocomplete="off" autofocus>
     <input name="day" type="number" placeholder="Day" max="31" min="1" autocomplete="off" autofocus>
     <input type="submit" value="Add Birthday">
```

En este punto lo que hacemos es crear la tabla donde iremos mostrando todos los cumpleaños de forma ordenada.
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
