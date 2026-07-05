mermaid
erDiagram
    Nomenclature {
        string CodeNomenclature PK "КодНоменклатуры"
        string Name "Наименование"
        string UnitOfMeasure "ЕдиницаИзмерения"
        string Group "ГруппаНоменклатуры"
        int ShelfLifeDefault "СрокГодностиПоУмолчанию (дни)"
    }

    Warehouse {
        string CodeWarehouse PK "КодСклада"
        string Name "НаименованиеСклада"
        string Address "Адрес"
        string Responsible "Ответственный"
    }

    Counterparty {
        string CodeCounterparty PK "КодКонтрагента"
        string Name "Наименование"
        string INN "ИНН"
        string Type "Тип (поставщик/покупатель)"
    }

    Batch {
        string CodeBatch PK "КодПартии"
        string CodeNomenclature FK "Номенклатура"
        string CodeWarehouse FK "Склад"
        date DateArrival "ДатаПоступления"
        decimal Quantity "Количество"
        string CodeCounterparty FK "Поставщик"
        date ShelfLife "СрокГодности"
    }

    Operation {
        string CodeOperation PK "КодОперации"
        string OperationType "ТипОперации (приход/расход)"
        string CodeBatch FK "Партия"
        decimal Quantity "Количество"
        datetime DateOperation "ДатаОперации"
        string DocBase "ДокументОснование"
        string CodeCounterparty FK "Контрагент"
    }

    Nomenclature ||--o{ Batch : "имеет"
    Warehouse ||--o{ Batch : "хранит"
    Counterparty ||--o{ Batch : "поставляет"
    Counterparty ||--o{ Operation : "участвует в"
    Batch ||--o{ Operation : "является основанием для"
