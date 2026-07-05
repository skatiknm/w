mermaid
erDiagram
    Culture {
        string CodeCulture PK "Код Культуры"
        string Name "Наименование"
        string Type "Тип Культуры"
        decimal NormYieldCGA "Нормативная Урожайность Ц/Га"
        decimal SeedDensity "Рекомендуемая Густота Посева Тыс Шт/Га"
        int SeedDepthCm "Глубина Заделки Семян См"
    }

    Field {
        string FieldNumber PK "Номер Поля"
        decimal AreaHA "Площадь Га"
        string SoilType "Тип Почвы"
        string District "Район"
        string CadastralNumber "Кадастровый Номер"
        int LastAgroChemYear "Год Последнего Агро Хим Обследования"
        int BonitetScore "Балл Бонитета"
    }

    Season {
        string SeasonCode PK "Код Сезона"
        int Year "Год"
        int SeasonSequence "Порядковый Номер Сезона"
        date StartDate "Дата Начала"
        date EndDate "Дата Окончания"
        string AgroClimateNotes "Агроклиматические Особенности"
    }

    Employee {
        string EmployeeTabNo PK "Табельный Номер"
        string FullName "ФИО"
        string Position "Должность"
        string Specialization "Специализация"
        string Phone "Телефон"
        date HireDate "Дата Приема На Работу"
    }

    AgroOperation {
        string OperationNumber PK "Номер Операции"
        string OperationType "Тип Операции"
        date OperationDate "Дата Проведения"
        string EmployeeTabNo FK "Табельный Номер Ответственного"
        string FieldNumber FK "Номер Поля"
        string SeasonCode FK "Код Сезона"
        string Equipment "Используемая Техника"
        decimal DoseRate "Дозировка Норма Внесения"
        decimal Cost "Стоимость Операции"
        string CodeCulture FK "КодКультуры (для посевов)"
    }

    YieldResult {
        string YieldResultCode PK "Код Результата"
        string FieldNumber FK "Номер Поля"
        string SeasonCode FK "Код Сезона"
        decimal ActualYieldCGA "Фактическая Урожайность ЦГа"
        decimal GrossHarvestC "Валовой СборЦ"
        decimal MoisturePercent "Влажность Зерна Проц"
        decimal WeedPercent "Засоренность Проц"
        string OperationHarvestNo FK "Номер Операци и Уборка"
        string Notes "Примечания"
    }

    Culture ||--o{ AgroOperation : "может высеваться в операциях типа «посев»"
    Field ||--o{ AgroOperation : "на поле выполняется множество агротехнических операций"
    Season ||--o{ AgroOperation : "в сезоне выполняется множество операций"
    Employee ||--o{ AgroOperation : "сотрудник выполняет множество операций"
    Field ||--o{ YieldResult : "для поля и сезона фиксируется один результат урожайности"
    Season ||--o{ YieldResult : "результат урожайности привязан к сезону"
    AgroOperation }|--|| YieldResult : "операция «уборка» обосновывает результат урожайности"
