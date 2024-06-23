```bsl 
ПараметрыСоединения = "
|DRIVER={MySQL ODBC 5.3 Unicode Driver};
|SERVER=crockid.ru;
|DATABASE=crockid_prod;
|UID=crockid_prod_ro;
|PWD=5oz@qdKSJKmPm;
|STMT=set character_set_results=cp1251;";


Connection = Новый COMОбъект("ADODB.Connection");
Connection.Open(ПараметрыСоединения);

RS = Новый COMОбъект("ADODB.Recordset");
RS.CursorType = 3;

RS.ActiveConnection=Connection;

RS.Open("SELECT crockid_prod.catalog_goods_remains.id AS id FROM crockid_prod.catalog_goods_remains where crockid_prod.catalog_goods_remains.amount > 0 or crockid_prod.catalog_goods_remains.amount_kem > 0");

RS.MoveFirst();

Пока RS.EOF()=0 Цикл
		Для Каждого стр Из RS.Fields Цикл
		Если стр.Name = "id" тогда
			Command = new COMObject("ADODB.Command");
			Command.CommandText = "UPDATE crockid_prod.catalog_goods_remains SET amount_kem = '0', amount = '0' where id = '" + XMLСтрока(стр.Value) + "';";
			Command.ActiveConnection = Connection;
			Command.CommandType = 1;
			Command.Execute();
		Конецесли;
	КонецЦикла;
	

	
	RS.MoveNext();
	
КонецЦикла;
RS.Close();
Connection.Close();


```