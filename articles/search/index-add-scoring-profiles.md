---
title: Повышение ранга поиска с помощью профилей оценки
titleSuffix: Azure Cognitive Search
description: Повышение оценок ранга поиска для Когнитивный поиск Azure путем добавления профилей оценки.
manager: nitinme
author: shmed
ms.author: ramero
ms.service: cognitive-search
ms.topic: conceptual
ms.date: 05/06/2020
ms.openlocfilehash: 97797e309c32c6ea996d5ae1901b9a266a683173
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2020
ms.locfileid: "91537639"
---
# <a name="add-scoring-profiles-to-an-azure-cognitive-search-index"></a>Добавление профилей повышения в индекс службы Когнитивного поиска Azure

*Оценка оценивает* оценку поиска для каждого элемента в упорядоченном результирующем наборе ранжирования. Каждому элементу в результирующем наборе поиска назначается оценка поиска (от наивысшей до наименьшей).

 Когнитивный поиск Azure использует оценку по умолчанию для вычисления начальной оценки, но вы можете настроить вычисление с помощью *профиля оценки*. Профили оценки позволяют управлять приоритетом элементов в результатах поиска. Например, может потребоваться повысить приоритет элементов на основе потенциального дохода, повысить уровень более новых элементов или, возможно, элементов, которые слишком долго находились на складе.  

 Следующий сегмент видео быстро пересылается по принципу работы профилей оценки в Azure Когнитивный поиск.
 
> [!VIDEO https://www.youtube.com/embed/Y_X6USgvB1g?version=3&start=463&end=970]

## <a name="scoring-profile-definitions"></a>Определения профиля оценки

 Профиль повышения — часть определения индекса, состоящая из взвешенных полей, функций и параметров.  

 В следующем примере показан простой профиль geo, который поможет вам получить представление о профиле оценки. Он повышает приоритет элементов, содержащих условие поиска в поле **hotelName**. Он также использует функцию `distance` для выбора элементов, которые находятся в пределах десяти километров от текущего расположения. Если кто-то ищет слово inn, которое входит в название отеля, документы, содержащие отели со словом inn, расположенные в пределах радиуса в 10 км от текущего расположения, будут показаны в результатах поиска выше.  


```json
"scoringProfiles": [
  {  
    "name":"geo",
    "text": {  
      "weights": {  
        "hotelName": 5
      }                              
    },
    "functions": [
      {  
        "type": "distance",
        "boost": 5,
        "fieldName": "location",
        "interpolation": "logarithmic",
        "distance": {
          "referencePointParameter": "currentLocation",
          "boostingDistance": 10
        }                        
      }                                      
    ]                     
  }            
]
```  


 Чтобы использовать этот профиль оценки, в строке запроса необходимо указать профиль. В следующем запросе обратите внимание на параметр `scoringProfile=geo`.  

```  
GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2020-06-30 
```  

 Этот запрос выполняет поиск слова inn и передает текущее расположение. Обратите внимание, что этот запрос включает другие параметры, такие как `scoringParameter` . Параметры запроса описаны в [документах поиска &#40;Azure Когнитивный поиск REST API&#41;](/rest/api/searchservice/Search-Documents).  

 Щелкните [Пример](#bkmk_ex) , чтобы просмотреть более подробный пример профиля оценки.  

## <a name="what-is-default-scoring"></a>Что такое оценка по умолчанию?  
 В процессе оценки вычисляется оценка поиска для каждого элемента в упорядоченном по рангу результирующем наборе. Каждому элементу в результирующем наборе поиска назначается оценка поиска (от наивысшей до наименьшей). Элементы с более высокой оценкой возвращаются приложению. По умолчанию возвращаются первые 50 элементов, но можно использовать параметр `$top` , чтобы вернуть меньше или больше элементов (до 1000 в одном ответе).  

Оценка поиска вычисляется на основе статистических свойств данных и запроса. Azure Когнитивный поиск находит документы, содержащие условия поиска в строке запроса (некоторые или все, в зависимости от `searchMode` ), что позволяет использовать документы, содержащие много экземпляров условия поиска. Оценка поиска возрастает, если условие поиска редко встречается в индексе данных, но часто — внутри документа. Базовый подход к вычислению релевантности называется [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf) или периодичностью терминов — инверсией документа.  

 Если предположить, что пользовательская сортировка не применяется, результаты ранжируются по оценке поиска, прежде чем они будут возвращены вызывающему приложению. Если параметр $top не указан, возвращаются 50 элементов с наивысшей оценкой поиска.  

 Значения оценки поиска в результирующем наборе могут повторяться. Например, может быть 10 элементов с оценкой 1,2, 20 элементов с оценкой 1,0 и 20 элементов с оценкой 0,5. Если у нескольких совпадений одинаковая оценка поиска, порядок сортировки элементов не определен и не является стабильным. Выполните запрос еще раз, и, возможно, позиции элементов изменятся. Если есть два элемента с одинаковой оценкой, невозможно определить, какой из них отобразится первым.  

## <a name="when-to-add-scoring-logic"></a>Когда следует добавлять логику оценки 
 Вам следует создать один или несколько профилей оценки, если ранжирование по умолчанию не соответствует вашим бизнес-целям. Например, вы можете решить, что при поиске следует предпочитать вновь добавленные элементы. Аналогично, у вас может быть поле, содержащее удельную прибыль, или другое поле, указывающее потенциальный доход. Повышение приоритета элементов, которые дают преимущества для бизнеса, может быть важным фактором при решении об использовании профилей оценки.  

 Упорядочивание на основе релевантности также реализуется с помощью профилей оценки. Рассмотрим страницы результатов поиска, которые вы использовали ранее, позволяющие сортировать данные по цене, дате, рейтингу или релевантности. В Когнитивный поиск Azure профили оценки выпускают параметр "релевантность". Определение релевантности контролируете вы в соответствии с бизнес-целями и типом результатов поиска, которые хотите предоставить.  

##  <a name="example"></a><a name="bkmk_ex"></a> Пример  
 Как отмечалось ранее, пользовательская оценка реализуется с помощью одного или нескольких профилей повышения, определенных в схеме индекса.  

 В этом примере показана схема индекса с двумя профилями оценки (`boostGenre`, `newAndHighlyRated`). Любой запрос к этому индексу, включающий профиль в качестве параметра запроса, будет использовать профиль для оценки результирующего набора.  

```json
{  
  "name": "musicstoreindex",  
  "fields": [  
    { "name": "key", "type": "Edm.String", "key": true },  
    { "name": "albumTitle", "type": "Edm.String" },  
    { "name": "albumUrl", "type": "Edm.String", "filterable": false },  
    { "name": "genre", "type": "Edm.String" },  
    { "name": "genreDescription", "type": "Edm.String", "filterable": false },  
    { "name": "artistName", "type": "Edm.String" },  
    { "name": "orderableOnline", "type": "Edm.Boolean" },  
    { "name": "rating", "type": "Edm.Int32" },  
    { "name": "tags", "type": "Collection(Edm.String)" },  
    { "name": "price", "type": "Edm.Double", "filterable": false },  
    { "name": "margin", "type": "Edm.Int32", "retrievable": false },  
    { "name": "inventory", "type": "Edm.Int32" },  
    { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }  
  ],  
  "scoringProfiles": [  
    {  
      "name": "boostGenre",  
      "text": {  
        "weights": {  
          "albumTitle": 1.5,  
          "genre": 5,  
          "artistName": 2  
        }  
      }  
    },  
    {  
      "name": "newAndHighlyRated",  
      "functions": [  
        {  
          "type": "freshness",  
          "fieldName": "lastUpdated",  
          "boost": 10,  
          "interpolation": "quadratic",  
          "freshness": {  
            "boostingDuration": "P365D"  
          }  
        },  
        {
          "type": "magnitude",  
          "fieldName": "rating",  
          "boost": 10,  
          "interpolation": "linear",  
          "magnitude": {  
            "boostingRangeStart": 1,  
            "boostingRangeEnd": 5,  
            "constantBoostBeyondRange": false  
          }  
        }  
      ]  
    }  
  ],  
  "suggesters": [  
    {  
      "name": "sg",  
      "searchMode": "analyzingInfixMatching",  
      "sourceFields": [ "albumTitle", "artistName" ]  
    }  
  ]   
}  
```  

## <a name="workflow"></a>Рабочий процесс  
 Чтобы реализовать пользовательское поведение оценки, добавьте профиль оценки в схему, которая определяет индекс. В индексе может быть до 100 профилей повышения (см. сведения в статье [Ограничения поиска Azure](search-limits-quotas-capacity.md)), но в одном запросе можно указать только один профиль.  

 Начните с [шаблона](#bkmk_template) , приведенного в этой статье.  

 Введите имя. Профили оценки не являются обязательными, но если вы добавите профиль, необходимо указать имя. Следуйте соглашениям об именовании полей (начинается с буквы, не содержит специальных символов и зарезервированных слов). Полный список см. в разделе [правила именования &#40;Azure Когнитивный поиск&#41;](/rest/api/searchservice/naming-rules) .  

 Текст профиля оценки состоит из взвешенных полей и функций.  

|||  
|-|-|  
|**Весов**|Укажите пары "имя — значение", которые назначают полю относительный вес. В [примере](#bkmk_ex) приоритет полей albumTitle, genre и artistName повышается на 1,5, 5 и 2 позиции соответственно. Почему для поля genre приоритет повышен намного больше, чем для других полей? Если поиск выполняется в однородных данных (как в случае с genre в `musicstoreindex`), вам может потребоваться большая вариативность в относительных весах. Например, в `musicstoreindex` "рок" появляется как жанр и в идентично сформулированных описаниях жанра. Если жанр должен обладать большим весом, чем описание жанра, полю genre потребуется назначить гораздо больший относительный вес.|  
|**Функции**|Используются, когда необходимы дополнительные вычисления для определенных контекстов. Допустимые значения: `freshness`, `magnitude`, `distance` и `tag`. Каждая функция имеет свои уникальные параметры.<br /><br /> -   `freshness` следует использовать, если вам необходимо повысить приоритет нового или старого элемента в зависимости от его "возраста". Эта функция может использоваться только с полями типа `datetime` (edm.DataTimeOffset). Обратите внимание, что `boostingDuration` атрибут используется только с `freshness` функцией.<br />-   `magnitude` следует применять, когда требуется повысить приоритет элементов на основе числового значения. К сценариям, в которых может вызваться эта функция, относится повышение приоритета на основе прибыли, наибольшей цены, наименьшей цены или числа загрузок. Эта функция может использоваться только с полями типа double и integer.<br />     Для функции `magnitude` можно задать обратный диапазон (от высоких оценок до низких), если результаты нужно отобразить в обратном порядке (например, повысить приоритет для элементов с более низкими ценами по сравнению с элементами с более высокими ценами). Если у вас есть диапазон цен от 100 до 1 доллара США, для параметров `boostingRangeStart` и `boostingRangeEnd` следует установить значения 100 и 1 соответственно, чтобы повысить приоритет для элементов с более низкими ценами.<br />-   `distance` следует применять, чтобы повысить приоритет по близости или географическому расположению. Эта функция может использоваться только с полями типа `Edm.GeographyPoint` .<br />-   `tag` следует применять, чтобы повысить приоритет по тегам, которые одновременно используются в документах и поисковых запросах. Эта функция может использоваться только с полями `Edm.String` и `Collection(Edm.String)`.<br /><br /> **Правила использования функции**<br /><br /> Тип функции (`freshness`, `magnitude`, `distance`), `tag` должен состоять из строчных букв.<br /><br /> Функции не могут содержать значения NULL или пустые значения. В частности, если добавить поле fieldname, для него необходимо указать значение.<br /><br /> Функции можно применять только к фильтруемым полям. Дополнительные сведения о фильтруемых полях см. в статье [Создание индекса &#40;Azure Когнитивный поиск REST API&#41;](/rest/api/searchservice/create-index) .<br /><br /> Функции могут применяться только к полям, определенным в коллекции полей индекса.|  

 После определения индекса выполните построение индекса, загрузив схему индекса и документы. Инструкции по этим операциям см. в статьях [Создание индекса &#40;Azure Когнитивный поиск REST API&#41;](/rest/api/searchservice/create-index) и [Добавление, обновление и удаление документов &#40;когнитивный Поиск Azure ](/rest/api/searchservice/addupdate-or-delete-documents) REST API&#41;. После построения индекса вы получите функциональный профиль оценки, который работает с данными поиска.  

##  <a name="template"></a><a name="bkmk_template"></a> Шаблон  
 В этом разделе показан синтаксис и шаблон для профилей оценки. Описание атрибутов см. в подразделе [Справочник по атрибутам индекса](#bkmk_indexref) в следующем разделе.  

```  
. . .   
"scoringProfiles": [  
  {   
    "name": "name of scoring profile",   
    "text": (optional, only applies to searchable fields) {   
      "weights": {   
        "searchable_field_name": relative_weight_value (positive #'s),   
        ...   
      }   
    },   
    "functions": (optional) [  
      {   
        "type": "magnitude | freshness | distance | tag",   
        "boost": # (positive number used as multiplier for raw score != 1),   
        "fieldName": "...",   
        "interpolation": "constant | linear (default) | quadratic | logarithmic",   

        "magnitude": {
          "boostingRangeStart": #,   
          "boostingRangeEnd": #,   
          "constantBoostBeyondRange": true | false (default)
        }  

        // ( - or -)  

        "freshness": {
          "boostingDuration": "..." (value representing timespan over which boosting occurs)   
        }  

        // ( - or -)  

        "distance": {
          "referencePointParameter": "...", (parameter to be passed in queries to use as reference location)   
          "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)   
        }   

        // ( - or -)  

        "tag": {
          "tagsParameter":  "..."(parameter to be passed in queries to specify a list of tags to compare against target field)   
        }
      }
    ],   
    "functionAggregation": (optional, applies only when functions are specified) "sum (default) | average | minimum | maximum | firstMatching"   
  }   
],   
"defaultScoringProfile": (optional) "...",   
. . .  
```  

##  <a name="index-attributes-reference"></a><a name="bkmk_indexref"></a> Справочник по атрибутам индекса  

> [!NOTE]  
>  Функция оценки может применяться только к фильтруемым полям.  

|attribute|Описание|  
|---------------|-----------------|  
|`name`|Обязательный элемент. Это имя профиля оценки. К нему применяются те же соглашения об именовании, что и к полям. Оно должно начинаться с буквы, не может содержать точки, двоеточия и символы "@", а также не может начинаться с фразы azureSearch (с учетом регистра).|  
|`text`|Содержит свойство Weights.|  
|`weights`|Необязательный параметр. Содержит пары «имя-значение», каждый из которых задает имя поля и относительный вес. Относительный вес должен быть положительным целым числом или числом с плавающей запятой.<br /><br /> Весовые коэффициенты используются для указания важности одного поля, доступного для поиска, относительно другого.|  
|`functions`|Необязательный параметр. Функция оценки может применяться только к фильтруемым полям.|  
|`type`|Требуется для функций оценки. Указывает тип используемой функции. Допустимые значения: magnitude, freshness, distance и tag. В каждый профиль оценки можно включить несколько функций. Имя функции должно состоять из строчных букв.|  
|`boost`|Требуется для функций оценки. Положительное число, используемое в качестве множителя для необработанной оценки. Не может быть равно 1.|  
|`fieldname`|Требуется для функций оценки. Функция оценки может применяться только к фильтруемым полям, входящим в коллекцию полей индекса. Кроме того, каждый тип функции накладывает дополнительные ограничения (freshness используется с полями типа datetime, magnitude — с полями типа integer или double, а distance — с полями типа location). В определении функции можно указать только одно поле. Например, чтобы использовать функцию magnitude дважды в одном профиле, необходимо добавить два определения magnitude (по одному для каждого поля).|  
|`interpolation`|Требуется для функций оценки. Определяет наклон для повышения приоритета оценки от начала до конца диапазона. Допустимые значения: Linear (по умолчанию), Constant, Quadratic и Logarithmic. Дополнительные сведения см. в разделе [Настройка интерполяций](#bkmk_interpolation).|  
|`magnitude`|Функция оценки magnitude используется для изменения рейтинга на основе диапазона значений для числового поля. Ниже приведены некоторые наиболее распространенные примеры.<br /><br /> -   **Рейтинги звезд:** Изменение оценки на основе значения в поле "Рейтинг". Если релевантны два элемента, первым отобразится элемент с более высокой оценкой.<br />-   **Поле:** Если два документа являются релевантными, розничный продавец может пожелать поднять документы с более высокими полями первыми.<br />-   **Щелкните счетчики:** Для приложений, которые отслеживаний щелчков мышью по действиям для продуктов или страниц, можно использовать величину для увеличения количества элементов, которые чаще всего будут получать наибольший объем трафика.<br />-   **Число Скачиваний:** Для приложений, которые отслеживаний загрузки, функция величины позволяет повысить уровень элементов, которые наиболее часто загружаются.|  
|`magnitude` &#124; `boostingRangeStart`|Задает начальное значение диапазона, на основе которого вычисляется результат функции magnitude. Значение должно быть целым числом или числом с плавающей запятой. Для оценок по звездам от 1 до 4 — 1. Для маржи более 50 % — 50.|  
|`magnitude` &#124; `boostingRangeEnd`|Задает конечное значение диапазона, на основе которого вычисляется результат функции magnitude. Значение должно быть целым числом или числом с плавающей запятой. Для оценок по звездам от 1 до 4 — 4.|  
|`magnitude` &#124; `constantBoostBeyondRange`|Допустимые значения: true или false (по умолчанию). Если задано значение true, к документам, содержащим значение целевого поля, превышающее верхнее ограничение диапазона, будет применяться максимальное повышение приоритета. Если задано значение false, эта функция не будет применяться к документам, содержащим значение целевого поля, которое не входит в диапазон.|  
|`freshness`|Функция оценки freshness используется для оценки ранжирования элементов на основе значений в полях `DateTimeOffset`. Например, элемент с более близкой датой может классифицироваться выше, чем старые элементы.<br /><br /> Кроме того, можно ранжировать такие элементы, как события календаря с будущими датами, в которых элементы ближе к текущей версии могут быть ранжированы выше по сравнению с элементами в будущем.<br /><br /> В текущем выпуске службы один конец диапазона фиксируется на текущее время. Чтобы повысить приоритет диапазона будущего времени, используйте отрицательное значение параметра `boostingDuration`. Чтобы повысить приоритет диапазона будущего времени, используйте отрицательное значение параметра `boostingDuration`.<br /><br /> рисунок ниже). Чтобы изменить направление коэффициента повышения приоритета, выберите коэффициент повышения приоритета меньше 1.|  
|`freshness` &#124; `boostingDuration`|Задает срок действия, после которого повышение приоритета перестает применяться для определенного документа. Синтаксис и примеры приведены далее в подразделе [Настройка boostingDuration](#bkmk_boostdur).|  
|`distance`|Функция оценки distance используется, чтобы изменить оценку документов на основе их близости к эталонному географическому расположению. Эталонное расположение предоставляется как часть запроса в параметре (с помощью параметра строки `scoringParameterquery`) в аргументе lon,lat.|  
|`distance` &#124; `referencePointParameter`|Параметр, который передается в запросах и используется в качестве эталонного расположения. `scoringParameter` — это параметр запроса. Описания параметров запроса см. в статье [Поиск документов &#40;Azure Когнитивный поиск REST API&#41;](/rest/api/searchservice/Search-Documents) .|  
|`distance` &#124; `boostingDistance`|Число, которое задает расстояние в километрах от эталонного расположения, где заканчивается диапазон повышения приоритета.|  
|`tag`|Функция оценки tag определяет оценку документов на основе тегов, имеющихся в документах и поисковых запросах. Документы, в которых имеются общие с поисковыми запросами теги, получают более высокий приоритет. Теги для каждого поискового запроса указываются в качестве параметра оценки (с помощью параметра строки `scoringParameterquery`).|  
|`tag` &#124; `tagsParameter`|Параметр, который передается в запросах для указания тегов определенного запроса. `scoringParameter` — это параметр запроса. Описания параметров запроса см. в статье [Поиск документов &#40;Azure Когнитивный поиск REST API&#41;](/rest/api/searchservice/Search-Documents) .|  
|`functionAggregation`|Необязательный параметр. Применяется, только если указаны функции. Допустимые значения: sum (по умолчанию), average, minimum, maximum и firstMatching. Оценка поиска — это одиночное значение, которое вычисляется на основе нескольких переменных, включая несколько функций. Эти атрибуты показывают, как значения повышения приоритета всех функций объединяются в единое агрегированное повышение приоритета, которое затем применяется к базовой оценке документа. Базовая оценка основана на значении [tf-idf](http://www.tfidf.com/), которое вычисляется на основе документа и поискового запроса.|  
|`defaultScoringProfile`|Если при выполнении поискового запроса профиль повышения не указан, используется оценка по умолчанию (только [tf-idf](http://www.tfidf.com/)).<br /><br /> Здесь можно задать имя профиля оценки по умолчанию, что приведет к тому, что Azure Когнитивный поиск будет использовать этот профиль, если в поисковом запросе не задан определенный профиль.|  

##  <a name="set-interpolations"></a><a name="bkmk_interpolation"></a> Задание интерполяций  
 Интерполяции позволяют задать форму наклона, используемого для оценки. Так как оценка идет по убыванию, наклон всегда снижается, но интерполяция определяет кривую нисходящего наклона. Можно использовать следующие типы интерполяции.  

| Интерполяции | Описание |  
|-|-|  
|`linear`|Для элементов, которые находятся в диапазоне от минимального до максимального значения, применяется постоянно убывающая величина. Линейная интерполяция — это интерполяция для оценки профиля по умолчанию.|  
|`constant`|Для элементов, которые находятся между начальным и конечным диапазонами, к результатам ранжирования применяется постоянное повышение приоритета.|  
|`quadratic`|По сравнению с линейной интерполяцией с постоянно убывающим повышением приоритета квадратичная интерполяционная функция сначала уменьшается не так быстро, а по мере приближения к конечному диапазону уменьшается на гораздо большую величину. Этот тип интерполяции невозможно использовать в функциях оценки tag.|  
|`logarithmic`|По сравнению с линейной интерполяцией с постоянно убывающим повышением приоритета логарифмическая интерполяционная функция сначала уменьшается быстрее, а по мере приближения к конечному диапазону уменьшается на гораздо меньшую величину. Этот тип интерполяции невозможно использовать в функциях оценки tag.|  

 ![Постоянные, линейные, квадратичные линии и линии log10 на графике](media/scoring-profiles/azuresearch_scorefunctioninterpolationgrapht.png "AzureSearch_ScoreFunctionInterpolationGrapht")  

##  <a name="set-boostingduration"></a><a name="bkmk_boostdur"></a> Настройка boostingDuration  
 `boostingDuration` — это атрибут функции `freshness`. Он задает срок действия, после которого повышение приоритета перестает применяться для определенного документа. Например, для повышения приоритета линейки продуктов или торговой марки в течение 10-дневного периода следует указать для соответствующих документов 10-дневный период как "P10D".  

 `boostingDuration` необходимо отформатировать как XSD-значение dayTimeDuration (ограниченное подмножество значения длительности ISO 8601). Для этого используется следующий шаблон: "P [nD] [T [nH] [nM] [nS]]".  

 Следующая таблица содержит несколько примеров.  

|Duration|boostingDuration|  
|--------------|----------------------|  
|1 день|"P1D"|  
|2 дня и 12 часов|"P2DT12H"|  
|15 минут|"PT15M"|  
|30 дней, 5 часов, 10 минут и 6,334 секунды|"P30DT5H10M6.334S"|  

 Дополнительные примеры см. в [документе о типах данных в схеме XML (веб-сайт W3.org)](https://www.w3.org/TR/xmlschema11-2/#dayTimeDuration).  

## <a name="see-also"></a>См. также  

+ [Справочник по REST API](/rest/api/searchservice/)
+ [Создание API индекса](/rest/api/searchservice/create-index)
+ [Библиотеки службы "Поиск Azure" для .NET](/dotnet/api/overview/azure/search?)