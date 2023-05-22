# Flask_final


Lo primero que hemos de hacer es descargar el archivo.zip que nos proporciona el tutorial, cuando lo tenemos descargado hemos de crear un proyecto al que lo podamos añadir.

Ahora lo que haremos sera ir analiando poco a poco los diferentes archivos que forman parte de nuestra aplicación.

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
