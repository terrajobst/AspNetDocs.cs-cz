> Některé příkazy se nepodporují, pokud aplikace jako úložiště dat identity používá SQLite. Z důvodu omezení v databázovém stroji `Alter` příkazy vyvolávají následující výjimku:
>
> System. NotSupportedException: SQLite nepodporuje tuto operaci migrace. 
>
> Jako alternativní řešení spusťte Code First migrace v databázi a změňte tabulky.
