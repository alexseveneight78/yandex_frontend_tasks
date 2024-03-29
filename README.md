# yandex_frontend_tasks

A. Время - деньги (15 баллов)
Коля изобрёл машину времени у себя в гараже и решил на этом заработать. Но так как он знает, что Организация Контроля Времени может забрать у него машину, он решил вести себя осторожнее и использовать рынок ценных бумаг в качестве источника дохода.
Он отправился в будущее, посмотрел там историю котировок по акциям компании FAIS. Компания примечательна тем, что один человек может держать только одну акцию. Но когда Коля увидел историю, он понял, что сам не сможет вычислить, когда нужно покупать акцию, а когда продавать. Тогда он обратился за помощью к вам, пообещав отдать половину заработанных денег.
Вам прекрасно известно, что за подобные махинации могут оштрафовать или даже посадить в тюрьму, и вы решили посчитать, стоит ли участвовать в этом. Вы уже решали подобную алгоритмическую задачу пару лет назад и смогли найти свой старый код. К сожалению, его производительности не хватает, чтобы посчитать результат за адекватное время.
Вам нужно оптимизировать представленную программу, которая вычисляет максимально возможный доход из всех возможных, опираясь на данные котировок. При этом не нужно учитывать деньги, которые тратятся на покупку акций, так как Коля собирается взять их со своего счёта.
Ваш старый код
Входные данные — массив чисел, каждое из которых отражает цену акции в конкретный день. Выходные данные — одно число, обозначающее максимально возможную прибыль.
var maxProfit = function (prices) {  
    return calculate(prices, 0);  
}  
 
function calculate(prices, index) {  
    if (index >= prices.length) {  
        return 0;  
    }  
 
    var maxProfix = 0;  
 
    for (var start = index; start < prices.length; start++) {  
        var localMaxProfit = 0;  
        for (var i = start + 1; i < prices.length; i++) {  
            if (prices[start] < prices[i]) {  
                var profit = calculate(prices, i + 1) + prices[i] - prices[start];  
                if (profit > localMaxProfit) {  
                    localMaxProfit = profit;  
                }  
            }  
        }  
 
        if (localMaxProfit > maxProfix)  
            maxProfix = localMaxProfit;  
    }  
    return maxProfix;  
}
Примеры работы
Пример 1
Вход: [71,11,51,31,61,41]
Выход: 70
Покупаем во второй день по цене 11 и продаём на третий день за 51, прибыль — 40. После этого покупаем за 31 в четвёртый день и продаем на пятый за 61, прибыль — 30. В итоге получаем прибыль 70.
Пример 2
Вход: [13,24,35,46,57]
Выход: 44
Покупаем в первый день, продаём в последний.
Пример 3
Вход: [700,612,445,343,10]
Выход: 0
Здесь вообще невозможно заработать, поэтому максимальная прибыль — 0.
Примечания
В качестве решения предоставьте файл, который экспортирует исправленный вариант функции maxProfit:
function maxProfit(prices) {  
  // ...  
}  
 
module.exports = maxProfit;
Решение будет запускаться в Nodejs 12.

B. Парсер событий (15 баллов)
Ограничение времени	1 секунда
Ограничение памяти	64Mb
Ввод	input.txt
Вывод	output.json
Менеджер Евгений решил сделать бота для популярного мессенджера, чтобы автоматически добавлять события в свой календарь. Раз в определенное время бот должен распознавать специально размеченный текст и отправлять его в сервис, который ожидает данные в специальном формате. В силу низкой квалификации в программировании Евгению нужна помощь с модулем, который принимает массив строк и формирует из них строку для сервиса календаря.
Формат ввода
В каждой строке название мероприятия содержится в кавычках, а дата — в одном из форматов:
DD.MM.YYYY, DD.MM.YY, DD/MM/YYYY, DD/MM/YY
Пример входных данных:
[  
  "В это воскресенье (22.09.2019) будет великолепное время, чтобы \"Пробежать марафон\".",  
  "А вот \"Садить деревья\" стоит на следующий день (23/09/19), ведь будет стоять жара."  
]
Могут быть и строки, в которых нет нужных данных. Такие строки следует игнорировать.
Формат вывода
Для примера выше должна вернуться строка:
"Пробежать марафон": 22.09.2019  
"Садить деревья": 23.09.19
Решение должно быть оформлено в виде commonJS-модуля:
module.exports = function(input) {  
 
}
 Набрать здесь Отправить файл

C. Идентификация котиков (40 баллов)
Сильный и независимый программист Вася держит дома 12 котов. Коты ходят гулять на улицу, и Вася хочет следить за тем, как каждый из них уходит и возвращается. Для этого Вася установил над дверцей для котов веб-камеру, которая делает фото, когда кот входит и выходит. Чтобы автоматически различать котов между собой, Вася придумал напечатать на их ошейниках баркоды, для отрисовки которых он придумал собственный алгоритм.
Помогите Васе написать функцию, которая отрисовывает баркод для ошейников его котов.
Формат информации о коте
Вася хранит информацию о котах в виде объектов:
type CatInfo = {  
    /**  
     * Кличка кота -  строка из маленьких и больших  
     * латинских букв и цифр, и пробелов (от 0 до 11 символов)  
     */  
    name: string;  
    /**  
     * Идентификатор кота - целое число от 0 до 255  
     */  
    id: number;  
    /**  
     *  Дата родждения кота в формате UNIX timestamp  
     */  
    birthday: number;  
}
Алгоритм отрисовки баркода
Баркоды, которые придумал Вася, выглядят так: 

 
В баркоде две основные секции: контент и контрольная сумма, ограниченные прямоугольниками шириной 7 пикселей с толщиной границы 3 пикселя.
Контент представляет собой 8 строк по 16 черных или белых квадратов в каждой строке (размер одного квадрата 8 на 8 пикселей), строки заполняются последовательно сверху вниз. Контрольная сумма — это столбец из 8 квадратов.
Белые квадраты в контенте кодируют 0, чёрные — 1.
Алгоритм формирования контента баркода
Поле name дополняется пробелами в конце до 11 символов и конвертируется в байтовый массив — каждому символу строки ставится соответствующий ASCII-код (число от 0 до 255).
Каждый элемент полученного массива переводится в двоичную запись (восемь сивмолов 0или 1) и кодируется последовательностью из восьми квадратов (0 — белый квардрат, 1 — чёрный квадрат). Квадраты отрисовываются в контенте баркода последовательно и построчно.
Далее поле id конвертируется в 8-битное двоичное число, которое кодируется последовательностью из восьми квадратов и дописывается в контент баркода.
Затем поле birthday переводится в 32-битное двоичное число, которое по такому же принципу кодируется квадратами и дописывается в конец баркода.
Алгоритм формирования контрольной суммы
Контрольная сумма вычисляется по строкам контента. Для отрисовки квадрата контрольной суммы определяется чётность суммы значений контента в соответствующей строке. Если значение чётное — в строке рисуется белый квадрат, в противном случае — чёрный.
Формат решения
Загружаемое вами решение должно содержать функцию renderBarcode:
/**  
 * Отрисовать баркод для кота  
 * @param catInfo {CatInfo} - информация о коте  
 * @param element {HTMLDivElement} - div с фиксированным размером 157x64 пикселей,  
 *     в который будет отрисовываться баркод  
 */  
function renderBarcode(catInfo, element) {  
    // ваш код  
}
Решение будет запускаться в браузере Google Chrome 77.
Примеры работы
Информация о коте:
{  
    "id": 185,  
    "name": "Murzick",  
    "birthday": 1164210686  
}
Баркод: 

 


Информация о коте:
{  
    "id": 96,  
    "name": "Ferdinand",  
    "birthday": 1429648740  
}
Баркод: 

 

D. Живая сталь (40 баллов)
На планете Ксетаксис живёт два племени огромных боевых человекоподобных роботов, которые уже давно воюют друг с другом.
Представители более развитой расы «космических жокеев» с другой планеты, которые сканируют Вселенную в поисках разумной жизни, установили, что в стародавние времена по планете прошёл компьютерный вирус, который изменил таблицы во внутренней документации некоторых роботов — с markdown-подобного внутреннего формата на HTML. Из-за этого общение между роботами было нарушено и разразилась война.
Помогите написать скрипт, который сконвертирует таблицы обратно во внутренний формат, понятный каждому роботу, и восстановит мир на планете. Роботы не должны страдать!
Вам нужно написать функцию, которая на вход принимает HTML таблицы и преобразует его в wiki-подобную разметку.
В качестве решения этого задания отправьте файл .js, в котором объявлена функция solution:
function solution(input) {  
    // ...  
}
Формат ввода
HTML таблицы приходит в виде строки:
<table>  
    <colgroup>  
        <col    align="right"    />  
        <col />  
        <col align="center"/>  
    </colgroup>  
    <thead>  
        <tr>  
            <td>Command    </td>  
            <td>    Description</td>  
            <th>Is implemented    </th>  
        </tr>  
    </thead>  
    <tbody>  
        <tr>  
            <th>git status   </th>  
            <td>   List all new or modified files</th>  
            <th>Yes   </th>  
        </tr>  
        <tr>  
            <th>git diff</td>  
            <td>Show file differences that have not been staged</td>  
            <td>No</td>  
        </tr>  
    </tbody>  
</table>
В таблице могут содержаться теги colgroup, thead и tbody в фиксированном порядке. 
Все эти теги опциональны, но всегда будет присутствовать как минимум thead либо tbody.
•	colgroup содержит теги col, у которых может быть опциональный атрибут align с одним из трёх значений (left|center|right)
•	thead и tbody содержат 1 или более tr
•	tr, в свою очередь, содержат как td, так и th
В таблице всегда будет хотя бы одна строка. 
В строке всегда будет хотя бы одна ячейка. 
В ячейке всегда присутствует хотя бы один не-whitespace символ.
Количество элементов th/td в строках всегда совпадает между всеми строками и с количеством элементов col в colgroup, при наличии colgroup.
Пробелы и переносы строк в исходном HTML могут встречаться в любом месте, не нарушающем валидность HTML.
Формат вывода
На выходе должна получиться строка с wiki-подобной разметкой:
^  Command ^ Description  ^  Is implemented  ^
^  git status | List all new or modified files  ^  Yes  |
^  git diff | Show file differences that have not been staged  |  No  |
Разделитель перед ячейкой таблицы выводится в зависимости от того, th это или td. 
Карет для th — ^, и вертикальная черта для td — |.
Все ячейки строк из thead должны быть разделены через карет вне зависимости от того, tdэто или th. 
Все строки, получившиеся из thead, должны завершаться каретом, а из tbody — вертикальной чертой.
Пробелы по краям содержимого тегов td и th должны быть удалены. 
Переносы строк в содержимом ячеек должны быть удалены. 
Более одного пробела подряд в содержимом ячеек должны быть заменены одним пробелом.
За выравнивание в ячейках столбцов результирующей wiki-подобной таблицы отвечают пробелы вокруг содержимого ячейки: 
| xxx  | два пробела справа и один слева значит выравнивание влево 
|  xxx  | два пробела по обоим сторонам значат выравнивание по центру 
|  xxx | два слева и один справа — по правому краю
При отсутствии заданного в теге col атрибута align выравнивание должно быть задано влево.
Примечания
•	Для перевода строки нужно использовать символ \n.
•	Решение будет проверяться в браузерном окружении (Chrome 78) с доступом к объектам document и window.
•	Можно использовать синтаксис до es2018 включительно.

E. Пандемия вируса (50 баллов)
Всемирная Организация Здравоохранения опубликовала доклад о признаках надвигающейся пандемии нового вируса, который угрожает фронтенд-разработчикам. Известно, что вирус никак не проявляет себя до тех пор, пока носитель не увидит js-код, содержащий некоторое выражение. Как только заражённый увидел это выражение, он теряет способность писать код на js и начинает непроизвольно писать код на фортране.
В докладе упоминается, что вирус активируется от взгляда на использование первого аргумента функции, передаваемой аргументом в вызов функции ‘Z.y.n‘, то есть заражённым нельзя показывать выражение, подобное ‘Z.y.n(function(a, b, c){console.log(a)})‘.
Чтобы не потерять случайно всех своих фронтендеров, в компании AST & Co решили проверить, содержит ли их код упомянутое выражение. Помогите инженерам компании написать такую проверку.
Про код в компании AST & Co известно, что:
•	он написан на es3,
•	переменные получают свои значения при декларации и не переписываются, т.е. в коде не будет подобного ‘var a = x; a = y;‘ и ‘var a = b = 1;‘,
•	обращение к свойствам объекта возможно как через точку, так и через скобки (‘a.b‘ и ‘a[’b’]‘),
•	часть выражения может быть сохранена в переменной, но никогда не передаётся в функцию параметром (‘a(x)‘ — запрещено),
•	нет функций, которые возвращают часть искомого выражения,
•	нет свойств объектов или элементов массивов, которые содержат часть выражения,
•	при обращении к свойству объекта, название свойства может быть взято из переменной (‘a[x]‘, x — переменная).
Проверка должна быть оформлена в виде CommonJS-модуля, который экспортирует функцию, принимающую на вход абстрактное синтаксическое дерево (ast) проверяемого кода.
Функция должна вернуть массив из ast-узлов, которые соответствуют местам использования первого параметра callback-функции, передаваемой аргументом в ‘Z.y.n‘. Порядок элементов в массиве не важен, дубли не допускаются.
module.exports = function (ast) {  
  ...  
  return [...];  
}
Ast получается из js-кода с помощью модуля @babel/parser версии 7.6.0.
const parser = require(’@babel/parser’),  
  ast = parser.parse(code);
Пример
Ввод	Вывод
{
  "type": "File",
  "start": 0,
  "end": 97,
  "program": {
    "type": "Program",
    "start": 0,
    "end": 97,
    "sourceType": "script",
    "interpreter": null,
    "body": [
      {
        "type": "ExpressionStatement",
        "start": 0,
        "end": 48,
        "expression": {
          "type": "CallExpression",
          "start": 0,
          "end": 47,
          "callee": {
            "type": "MemberExpression",
            "start": 0,
            "end": 5,
            "object": {
              "type": "MemberExpression",
              "start": 0,
              "end": 3,
              "object": {
                "type": "Identifier",
                "start": 0,
                "end": 1,
                "name": "Z"
              },
              "property": {
                "type": "Identifier",
                "start": 2,
                "end": 3,
                "name": "y"
              },
              "computed": false
            },
            "property": {
              "type": "Identifier",
              "start": 4,
              "end": 5,
              "name": "n"
            },
            "computed": false
          },
          "arguments": [
            {
              "type": "FunctionExpression",
              "start": 6,
              "end": 46,
              "id": null,
              "generator": false,
              "async": false,
              "params": [
                {
                  "type": "Identifier",
                  "start": 16,
                  "end": 17,
                  "name": "a"
                }
              ],
              "body": {
                "type": "BlockStatement",
                "start": 19,
                "end": 46,
                "body": [
                  {
                    "type": "ReturnStatement",
                    "start": 25,
                    "end": 44,
                    "argument": {
                      "type": "Identifier",
                      "start": 42,
                      "end": 43,
                      "name": "a"
                    }
                  }
                ],
                "directives": []
              }
            }
          ]
        }
      },
      {
        "type": "ExpressionStatement",
        "start": 50,
        "end": 96,
        "expression": {
          "type": "CallExpression",
          "start": 50,
          "end": 95,
          "callee": {
            "type": "MemberExpression",
            "start": 50,
            "end": 55,
            "object": {
              "type": "MemberExpression",
              "start": 50,
              "end": 53,
              "object": {
                "type": "Identifier",
                "start": 50,
                "end": 51,
                "name": "Z"
              },
              "property": {
                "type": "Identifier",
                "start": 52,
                "end": 53,
                "name": "y"
              },
              "computed": false
            },
            "property": {
              "type": "Identifier",
              "start": 54,
              "end": 55,
              "name": "n"
            },
            "computed": false
          },
          "arguments": [
            {
              "type": "FunctionExpression",
              "start": 56,
              "end": 94,
              "id": null,
              "generator": false,
              "async": false,
              "params": [
                {
                  "type": "Identifier",
                  "start": 66,
                  "end": 67,
                  "name": "x"
                }
              ],
              "body": {
                "type": "BlockStatement",
                "start": 69,
                "end": 94,
                "body": [
                  {
                    "type": "ExpressionStatement",
                    "start": 75,
                    "end": 92,
                    "expression": {
                      "type": "CallExpression",
                      "start": 75,
                      "end": 91,
                      "callee": {
                        "type": "MemberExpression",
                        "start": 75,
                        "end": 86,
                        "object": {
                          "type": "Identifier",
                          "start": 75,
                          "end": 82,
                          "name": "console"
                        },
                        "property": {
                          "type": "Identifier",
                          "start": 83,
                          "end": 86,
                          "name": "log"
                        },
                        "computed": false
                      },
                      "arguments": [
                        {
                          "type": "StringLiteral",
                          "start": 87,
                          "end": 90,
                          "extra": {
                            "rawValue": "x",
                            "raw": "'x'"
                          },
                          "value": "x"
                        }
                      ]
                    }
                  }
                ],
                "directives": []
              }
            }
          ]
        }
      }
    ],
    "directives": []
  }
}	[
  {
    "type": "Identifier",
    "start": 42,
    "end": 43,
    "name": "a"
  }
]
Примечания
Следующий код можно взять за основу для обхода дерева.
/**  
 * Функция обхода дерева. Выполняет обход дерева в глубину,  
 * передаваяв callback-функции onNodeEnter (до посещения потомков)  
 * и onNodeLeave (после посещения потомков) каждый узел дерева  
 * и текущую область видимости (смотри определение Scope ниже)  
 *  
 * @param      {object}    ast                              Исходное ast  
 * @param      {Function}  [onNodeEnter=(node, scope)=>{}]  Вызывается для каждого узла до посещения потомков  
 * @param      {Function}  [onNodeLeave=(node, scope)=>{}]  Вызывается для каждого узла после посещения потомков  
 */  
function traverse(  
    ast,  
    onNodeEnter = (node, scope) => {},  
    onNodeLeave = (node, scope) => {}  
) {  
    const rootScope = new Scope(ast);  
 
    _inner(ast, rootScope);  
 
    /**  
     * Определение области видимости узла.  
     * Может либо вернуть текущий scope, либо создать новый  
     *  
     * @param      {object}  astNode       ast-узел  
     * @param      {Scope}   currentScope  текущая область видимости  
     * @return     {Scope}   область видимости для внутренних узлов astNode  
     */  
    function resolveScope(astNode, currentScope) {  
        let isFunctionExpression = ast.type === ’FunctionExpression’,  
            isFunctionDeclaration = ast.type === ’FunctionDeclaration’;  
 
        if (!isFunctionExpression &&  
            !isFunctionDeclaration) {  
            // Новые области видимости порждают только функции  
            return currentScope;  
        }  
 
        // каждая функция порождает новую область видимости  
        const newScope = new Scope(ast, currentScope);  
 
        ast.params.forEach(param => {  
            // параметры функции доступны внутри функции  
            newScope.add(param.name);  
        });  
 
        if (isFunctionDeclaration) {  
            // имя функции при декларации доступно снаружи функции  
            currentScope.add(ast.id.name);  
        } else {  
            // имя функции-выражения доступно только внутри неё  
            newScope.add(ast.id.name);  
        }  
 
        return newScope;  
    }  
 
    /**  
     * Рекурсивная функция обхода ast  
     *  
     * @param      {object}  astNode  Текущий ast-узел  
     * @param      {Scope}  scope     Область видимости для текущего ast-узла  
     */  
    function _inner(astNode, scope) {  
        if (Array.isArray(astNode)) {  
            astNode.forEach(node => {  
                /* Рекурсивный обход элементов списков.  
                 * Списками являются, например, параметры функций  
                 */  
                _inner(node, scope);  
            });  
        } else if (astNode && typeof astNode === ’object’) {  
            onNodeEnter(astNode, scope);  
 
            const innerScope = resolveScope(astNode, scope),  
                keys = Object.keys(astNode).filter(key => {  
                    // loc - служебное свойство, а не ast-узел  
                    return key !== ’loc’ &&  
                        astNode[key] && typeof astNode[key] === ’object’;  
                });  
 
            keys.forEach(key => {  
                // Обход всех потомков  
                _inner(astNode[key], innerScope);  
            });  
 
            onNodeLeave(astNode, scope);  
        }  
    }  
}  
 
/**  
 * Представление области видимости  
 *  
 * @class      Scope (name)  
 * @param      {object}  astNode      ast-узел, породивший эту область видимости  
 * @param      {object}  parentScope  Родительская область видимости  
 */  
function Scope(astNode, parentScope) {  
    this._node = astNode;  
    this._parent = parentScope;  
    this._vars = new Set();  
}  
 
Scope.prototype = {  
    /**  
     * Добавление имени переменной в область видимости  
     *  
     * @param      {string}  name    имя переменной  
     */  
    add(name) {  
        this._vars.add(name);  
    },  
    /**  
     * Была ли определена переменная с таким именем.  
     *  
     * @param      {string}   name    имя переменной  
     * @return     {boolean}  Встречалась ли переменная с таким именем в доступных областях видимости  
     */  
    isDefined(name) {  
        return this._vars.has(name) || (this._parent && this._parent.isDefined(name));  
    }  
};  


F. Галактический коллектор (60 баллов)
Степан работает галактическим коллектором — собирает долги за ЖКХ по всей галактической Империи. Степану нравится его работа. Она дает возможность побывать в таких местах, куда в другой ситуации он никогда бы не попал. Море впечатлений и новых знакомств!
Степану приходится часто перелетать с одной планеты на другую. Планеты вращаются по разным орбитам, поэтому на каждой планете собственный счёт времени. Секунды везде текут одинаково, но на разных планетах разное количество секунд в минуте, минут в часе, часов в сутках (но сутки всегда равны двум оборотам часовой стрелки). Также считается, что в прошлом была Точка начала отсчёта времени, в которой время на всех планетах было равно 0 (0 часов, 0 минут, 0 секунд).
Пожалуйста, сделайте для Степана часы, которые могут переключаться между временем разных планет. Для этого вы можете использовать JavaScript и js-фреймворк под названием Framework.
Часы должны иметь три стрелки: часовую, минутную и секундную. В аргументах конструктора приходят параметры времени для планет и текущее время (количество секунд, прошедших от точки отсчета). Часы должны иметь кнопку переключения (циклического) между временем планет. При переводе стрелок можно двигать их по часовой стрелке или против неё (по наикратчайшему пути).
При включении часов все стрелки указывают на значение 0. Необходимо кратчайшим путем перевести стрелки в положение, соответствующее указанному времени (параметр time) на первой планете из списка.
Пример кода прошивки часов
const ONE_SECOND_DEGREES = 6;  
const ONE_SECOND_FACTOR = 1 / Framework.SPEED * ONE_SECOND_DEGREES;  
 
class MyClock extends Framework.Clock {  
    constructor() {  
        super();  
 
        this.arrows.push(new Framework.Arrow("seconds", {  
            color: "red"  
        }));  
 
        this.arrows.push(new Framework.Arrow("minutes", {  
            weight: 3,  
            length: 80  
        }));  
 
        this.arrows.push(new Framework.Arrow("hours", {  
            weight: 3,  
            length: 60  
        }));  
 
        this.buttons.push(new Framework.Button("A", () => {  
            alert("A");  
        }));  
 
        this.tick = 0;  
    }  
 
    onBeforeTick() {  
        const [arrow] = this.arrows;  
 
        this.tick++;  
 
        arrow.rotateFactor = this.tick % 10 ? 0 : ONE_SECOND_FACTOR;  
 
        console.log("before: " + arrow.pos);  
    }  
 
    onAfterTick() {  
        const [arrow] = this.arrows;  
 
        console.log("after: " + arrow.pos);  
    }  
}
Формат параметров конструктора
// текущее время (количество секунд от точки отсчета времени)  
const time = 1267457;  
 
// параметры планет  
// h — количество часов в одном обороте стрелки  
// m — количество минут в часе  
// s — количество секунд в минуте  
const planets = [  
    { h: 4, m: 20, s: 10 },  
    { h: 12, m: 60, s: 60 }  
];  
 
const app = new MyClock({ planets, time });
Пример
Ввод	Вывод
{
    "comments": "положение стрелок",
    "steps": [
        { "ticks": 10 }, 
        { "button": 0, "ticks": 10 },
        { "button": 0, "ticks": 10 }
    ],
    "params": {
        "time": 615,
        "planets": [
            { "h": 6, "m": 30, "s": 30 },
            { "h": 12, "m": 60, "s": 60 }
        ]
    }
}	[
  {
    "seconds": 192,
    "minutes": 240,
    "hours": 0
  },
  {
    "seconds": 102,
    "minutes": 60,
    "hours": 0
  },
  {
    "seconds": 216,
    "minutes": 240,
    "hours": 0
  }
]
Примечания
Откройте HTML-файл тестовой страницы по ссылке «Скачать условие задачи» в конце описания. Вам нужно написать на JavaScript класс с названием MyClock, который реализует поведение, описанное в условии.
class MyClock extends Framework.Clock {  
    // ваш код  
}
При проверке, файл с вашим решением будет подключен на тестовую страницу в место, обозначенное комментарием:
<!-- в качестве решения предоставьте файл solution.js -->  
<script src="solution.js"></script>
Идентификаторы стрелок (первый параметр их конструктора) должны быть такими же, как в примере: "seconds", "minutes", "hours".
Ваше решение будет тестироваться в браузере Google Chrome 77.


