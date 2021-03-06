<h1>BOM</h1>

<p>
  Основным инструментом работы и динамических изменений на странице является DOM (Document Object Model) – объектная модель, используемая для XML/HTML-документов. C помощью объектной модели браузера (BOM) возможно управление поведением браузера из JavaScript. BOM включает в себя несколько объектов.
</p>

<h2>Window</h2>
<p>
  Объект window представляет собой окно содержащее DOM документ; свойство document указывает на DOM document загруженный в данном окне. Окно текущего документа может быть получено используя `document.defaultView` свойство.
</p>
<p>
  <strong>Объект window является корневым объектом JavaScript.</strong> Все объекты JavaScript, а также переменные и функции определяемые пользователем хранятся в объекте window. Объект Window в клиентском JavaScript является глобальным объектом. Это означает, что объект Window находится на вершине цепочки областей видимости и что его свойства и методы фактически являются глобальными переменными и функциями. Объект Window имеет свойство window, которое всегда ссылается на сам объект. Это свойство можно использовать для ссылки на сам объект, но обычно в этом нет необходимости, если требуется просто сослаться на свойство глобального объекта окна.
</p>
<h3>Свойства</h3>
<table>
  <tr>
    <th>Свойство</th>
    <th>Описание</th>
  </tr>
  <tr>
    <td>closed</td>
    <td>Возвращает логическое значение (true или false) в зависимости от того, закрыто указанное окно или отрыто.</td>
  </tr>
</table>

```js
var newwin = window.open();

if (newwin.closed) {
  document.getElementById("mes").innerHTML = "Окно newwin было закрыто.";
} else {
  document.getElementById("mes").innerHTML = "Окно newwin открыто в данный момент.";
}
```
<table>
  <tr>
    <td rowspan="3">frames</td>
    <td>
      Возвращает массив всех фреймов на странице (включая <strong>iframe</strong>). Элемент <strong>iframe</strong> является обычным узлом DOM, как и любой другой. Существенное отличие – в том, что с ним связан объект <strong>window</strong> внутреннего окна. Он доступен по ссылке <strong>iframe.contentWindow</strong>. Таким образом, <strong>frame.contentWindow.document</strong> будет внутренним документом, <strong>iframe.contentWindow.document.body</strong> – его <strong>body</strong> и так далее. Элемент <strong>iframe</strong> является «двуличным». С одной стороны, это обычный узел DOM, с другой – внутри находится окно, которое может иметь совершенно другой URL, содержать независимый документ из другого источника. Внешний документ имеет полный доступ к <strong>iframe</strong> как к DOM-узлу. А тот к окну – если они с одного источника. Это приводит к забавным последствиям. Например, чтобы узнать об окончании загрузки <strong>iframe</strong>, мы можем повесить обработчик <strong>iframe.onload</strong>. По сути, это то же самое что <strong>iframe.contentWindow.onload</strong>, но его мы можем поставить лишь в случае, если окно с того же источника. Альтернативный способ доступа к окну фрейма – это получить его из коллекции <strong>window.frames</strong>.
    </td>
  </tr>
  <tr>
    <td>
      <h3>Есть два способа доступа:</h3>
      <strong>window.frames[0]</strong> доступ по номеру.
      <strong>window.frames.iframeName</strong> доступ по name ифрейма. Обратим внимание: в коллекции хранится именно окно (<strong>contentWindow</strong>), а не DOM-элемент. Внутри фрейма могут быть свои вложенные фреймы. Всё это вместе образует иерархию.
    </td>
  </tr>
  <tr>
    <td>
      <h3>Ссылки для навигации по ней:</h3>
      window.frames коллекция «детей» (вложенных ифреймов) window.parent содержит ссылку на  родительское окно, позволяет обратиться к нему из ифрейма. window.top содержит ссылку на самое верхнее окно (вершину иерархии). Свойство <strong>top</strong> позволяет легко проверить, во фрейме ли находится текущий документ:
    </td>
  </tr>
</table>

```js
if (window == top) {
  alert( 'Этот скрипт выполняется в окне верхнего уровня' );
} else {
  alert( 'Этот скрипт исполняется во фрейме или дочернем окне!');
}
```

<table>
  <tr>
    <td>document</td>
    <td>Возвращает объект <strong>Document</strong> данного окна.</td>
  </tr>
  <tr>
    <td>history</td>
    <td>Возвращает объект <strong>History</strong> данного окна.</td>
  </tr>
  <tr>
    <td>length</td>
    <td>Возвращает количество фреймов (включая <strong>iframe</strong>), которые находятся в данном окне.</td>
  </tr>
  <tr>
    <td>location</td>
    <td>Возвращает объект <strong>Location</strong> данного окна.</td>
  </tr>
  <tr>
    <td>name</td>
    <td>Устанавливает или возвращает имя данного окна.</td>
  </tr>
  <tr>
    <td>navigator</td>
    <td>Возвращает объект <strong>Navigator</strong> данного окна.</td>
  </tr>
  <tr>
    <td>opener</td>
    <td>Возвращает ссылку на окно, которое открыло данное.</td>
  </tr>
  <tr>
    <td>parent</td>
    <td>Возвращает родительское окно данного окна.</td>
  </tr>
  <tr>
    <td>screen</td>
    <td>Возвращает объект <strong>Screen</strong> данного окна.</td>
  </tr>
  <tr>
    <td>self</td>
    <td>Возвращает текущее окно.</td>
  </tr>
  <tr>
    <td>top</td>
    <td>Возвращает верхнее браузерное окно для данного окна.</td>
  </tr>
</table>

<h3>Методы</h3>
<table>
  <tr>
    <th>Метод</th>
    <th>Описание</th>
  </tr>
  <tr>
    <td>alert()</td>
    <td>Вызывает окно оповещения, которое содержит текст сообщения и клавишу ОК.</td>
  </tr>
  <tr>
    <td>blur()</td>
    <td>Делает окно неактивным.</td>
  </tr>
  <tr>
    <td>clearInterval()</td>
    <td>Прекращает повторное выполнение кода заданного setInterval().</td>
  </tr>
  <tr>
    <td>clearTimeout()</td>
    <td>Отменяет запланированное методом setTimeout() выполнение кода.</td>
  </tr>
  <tr>
    <td>close()</td>
    <td>Закрывает окно.</td>
  </tr>
  <tr>
    <td>confirm()</td>
    <td>Вызывает окно подтверждения содержащее текст сообщения и клавиши ОК и Отмена.</td>
  </tr>
</table>
```js
// Выведем окно подтверждения и запишем результат в переменную x
var x = confirm("Нажмите ОК или Отмена.");

// Если пользователь нажал ОКif (x == true) {
  document.getElementById("mes").innerHTML = "Вы нажали кнопку ОК."
} else{ //Если пользователь нажал Отмена
  document.getElementById("mes").innerHTML = "Вы нажали кнопку Отмена."
}
```
<table>
  <tr>
    <td>focus()</td>
    <td>Делает окно активным.</td>
  </tr>
  <tr>
    <td>moveBy()</td>
    <td>Смещает окно относительно его текущей позиции.</td>
  </tr>
  <tr>
    <td>moveTo()</td>
    <td>Перемещает окно на указанную позицию.</td>
  </tr>
  <tr>
    <td>open()</td>
    <td>Открывает новое окно браузера. <strong>open(URL,имя,параметры)</strong> Имя, устанавливает имя окна Является не обязательным параметром. Указывает способ открытия или имя окна. 
    <h4>Возможные значения:</h4>
      <ul>
        <li><strong>_blank URL</strong> загружается в новом окне</li>
        <li><strong>_parent URL</strong> загружается в родительском фрейме</li>
        <li><strong>_self URL</strong> заменяет текущую страницу</li>
      </ul>
      <h4>Параметры отделенные запятой. Доступны следующие параметры:</h4>
      <ul>
        <li><strong>height</strong> устанавливает высоту окна в пикселях. Минимальное значение 100.</li>
        <li><strong>location</strong> отвечает за отображение адресной строки (yes - отображать, no - неотображать).</li>
        <li><strong>menubar URL</strong> отвечает за отображение верхнего меню (yes - отображать, no - неотображать).</li>
        <li><strong>resizable</strong> отвечает за возможность изменения размеров окна (yes - можно изменять размер, no - нельзя изменять размер).</li>
        <li><strong>scrollbars</strong> отвечает за отображения полосы прокрутки (yes - отображать, no - неотображать).</li>
        <li><strong>width</strong> устанавливает ширину окна в пикселях. Минимальное значение 100.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>print()</td>
    <td>Распечатывает содержимое текущего окна.</td>
  </tr>
  <tr>
    <td>prompt()</td>
    <td>Вызывает окно запроса, побуждающее посетителя ввести в него определенные данные.</td>
  </tr>
</table>
```js
//Выведем окно запроса и запишем результат (введенные пользователем данные) в переменную x
var x = prompt('Введите Ваше имя:', 'Имя');

//Выведем введенные пользователем данные на страницу
document.getElementById("mes").innerHTML = x;
```
<table>
  <tr>
    <td>scrollBy()</td>
    <td>Прокручивает содержимое окна на указанное количество пикселей.</td>
  </tr>
  <tr>
    <td>scrollTo()</td>
    <td>Прокручивает содержимое окна до указанных координат.</td>
  </tr>
  <tr>
    <td>setInterval()</td>
    <td>Вызывает функцию или выполняет код через определенные промежутки времени (указанные в миллисекундах).</td>
  </tr>
  <tr>
    <td>setTimeout()</td>
    <td>Вызывает функцию или выполняет код после указанного количества миллисекунд один раз.</td>
  </tr>
</table>

<h2>Document</h2>
<p>С помощью данного объекта Вы сможете добавлять, изменять и удалять HTML элементы на странице из скриптов.</p>

<h3>Свойства</h3>

<table>
  <tr>
    <th>Свойство</th>
    <th>Описание</th>
  </tr>
  <tr>
    <td>cookie</td>
    <td>Возвращает <strong>cookie</strong> связанные с данным документом. Куки - это небольшой объем данных, которые хранятся вэб браузером. Они позволяют Вам сохранять определенную информацию о пользователе и получать ее каждый раз, когда он посещает Вашу страницу. Каждый пользователь имеет свой собственный уникальный набор куков. Обычно куки используются веб сервером для выполнения таких функций как отслеживание посещений сайта, регистрации на сайте и сохранения сведений о заказах или покупках. Однако нам не нужно придумывать программу для вэб сервера чтобы использовать куки. Мы можем использовать их с помощью JavaScript. Создать куки можно следующим образом:</td>
  </tr>
</table>
```js
document.cookie = "name=значение; expires=дата; path=путь; domain=домен; secure";
// получить весь сохраненный набор куков так:
var x = document.cookie;
```
<table>
  <tr>
    <td>Для сохранения куки нужно присвоить document.cookie текстовую строку, которая содержит свойства куки, которые мы хотим создать:</td>
  </tr>
</table>
```js
document.cookie = "name=значение; expires=дата; path=путь; domain=домен; secure";
// expires=дата
// document.cookie // список все кук в виде строки имя=значение; имя=значение;
// document.cookie.split("; ").forEach(cookie => console.log(cookie.split("=")))
```
<table>
  <tr>
    <td></td>
    <td>Устанавливает дату истечения срока хранения куки. Дата должна быть представлена в формате, который возвращает метод <strong>toGMTString()</strong> объекта <strong>Date</strong>. Если значение expires не задано, куки будет удалено при закрытии браузера.
<h5>path=путь</h5>
<p>Данная опция устанавливает путь на сайте, в рамках которого действует куки. Получить значение куки могут только документы из указанного пути. Обычно данное свойство оставляют пустым, что означает что только документ установивший куки может получит доступ к нему.</p>
<h5>domain=домен</h5>
<p>Данная опция устанавливает домен, в рамках которого действует куки. Получить значение куки могут только сайты из указанного домена. Обычно данное свойство оставляют пустым, что означает, что только домен установивший куки может получит доступ к нему.</p>
<h5>expires</h5>
<p>время жизни (указывается дата в UTC). Если не указать, то cookie-элемент удалится сразу после закрытия окна со страницей</p>
<h5>secure</h5>
<p>Данная опция указывает браузеру, что для пересылки куки на сервер следует использовать SSL. Очень редко используется. удаление куки из браузера происходит посредством установки срока хранения на одну секунду раньше текущего значения времени.</p>
    </td>
  </tr>
  <tr>
    <td>document.doctype</td>
    <td>Позволяет узнать doctype документа.</td>
  </tr>
  <tr>
    <td>domain</td>
    <td>Возвращает доменное имя сервера, на котором  размещается данный документ.</td>
  </tr>
</table>
```js
document.write(document.domain);
```
<table>
  <tr>
    <td>forms</td>
    <td>Возвращает массив содержащий все формы имеющиеся на странице.</td>
  </tr>
  <tr>
    <td>images</td>
    <td>Возвращает массив содержащий все картинки имеющиеся на странице.</td>
  </tr>
  <tr>
    <td>links</td>
    <td>Возвращает массив содержащий все ссылки имеющиеся на странице.</td>
  </tr>
  <tr>
    <td>document.readyState</td>
    <td>Позволяет узнать статус загрузки документа.</td>
  </tr>
  <tr>
    <td>URL</td>
    <td>Возвращает текущий URL.</td>
  </tr>
</table>

<h2>Screen</h2>
<p>Объект <strong>Screen</strong> содержит информацию об экране пользователя. С помощью свойств данного объекта Вы можете узнать какое разрешение, а также какая глубина цвета установлена на экране пользователя. Свойство <strong>width</strong> определяет ширину экрана пользователя, а свойство <strong>height</strong> высоту.
</p>

<h3>Свойства</h3>

<table>
  <tr>
    <th>Свойство</th>
    <th>Описание</th>
  </tr>
  <tr>
    <td>availHeight</td>
    <td>Возвращает высоту экрана (исключая такие элементы интерфейса как полоса прокрутки, строка состояния, панель инструментов и т.д.).
    </td>
  </tr>
  <tr>
    <td>availWidth</td>
    <td>Возвращает ширину экрана (исключая такие элементы интерфейса как полоса прокрутки, строка состояния, панель инструментов и т.д.).
    </td>
  </tr>
  <tr>
    <td>colorDepth</td>
    <td>Возвращает битовую глубину цветовой палитры для отображения изображений.</td>
  </tr>
  <tr>
    <td>height</td>
    <td>Возвращает общую высоту экрана.</td>
  </tr>
  <tr>
    <td>width</td>
    <td>Возвращает общую ширину экрана.</td>
  </tr>
</table>

<h2>Navigator</h2>
<p>С помощью объекта navigator Вы можете определить какой браузер использует пользователь. Так же с помощью navigator Вы можете проверить может ли пользователь принимать cookie и включена ли у него поддержка Java.</p>
```js
document.addEventLister("online" ...) // Что сделать при включении интернета
document.addEventLister("ofline" ...) // Что сделать при отключении интернета

"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36"

navigator.userAgent.indexOf("MSIE") // -1 // ie ли это
```

<h3>Свойства</h3>
<table>
  <tr>
    <th>Свойство</th>
    <th>Описание</th>
  </tr>
  <tr>
    <td>appCodeName</td>
    <td>Позволяет узнать кодовое имя браузера.</td>
  </tr>
  <tr>
    <td>appName</td>
    <td>Позволяет узнать имя браузера.</td>
  </tr>
  <tr>
    <td>appVersion</td>
    <td>Позволяет узнать версию браузера.</td>
  </tr>
  <tr>
    <td>cookieEnabled</td>
    <td>Проверяет включена или нет поддержка cookie у пользователя.</td>
  </tr>
  <tr>
    <td>platform</td>
    <td>Позволяет узнать платформу, под которую скомпилирован браузер пользователя (т.е. фактически узнать ОС, которую использует пользователь).</td>
  </tr>
  <tr>
    <td>userAgent</td>
    <td>Возвращает полную информацию о браузере пользователя (возвращает заголовок, который посылает браузер во время запроса страницы).</td>
  </tr>
</table>

<h2>Location</h2>
<p>С помощью объекта location Вы можете узнать любую информацию о URL текущего документа.</p>

<h3>Свойства</h3>
<table>
  <tr>
    <th>Свойство</th>
    <th>Описание</th>
  </tr>
  <tr>
    <td>hash</td>
    <td>Возвращает часть URL начиная со знака #</td>
  </tr>
  <tr>
    <td>host</td>
    <td>Возвращает часть URL содержащую домен сайта.</td>
  </tr>
  <tr>
    <td>href</td>
    <td>Возвращает URL целиком.</td>
  </tr>
  <tr>
    <td>pathname</td>
    <td>Возвращает часть URL содержащую путь к загруженному документу.
    </td>
  </tr>
  <tr>
    <td>protocol</td>
    <td>Возвращает часть URL содержащую название протокола.</td>
  </tr>
  <tr>
    <td>search</td>
    <td>Возвращает часть URL начиная со знака ?</td>
  </tr>
</table>

<h3>Методы</h3>

<table>
  <tr>
    <th>Метод</th>
    <th>Описание</th>
  </tr>
  <tr>
    <td>reload()</td>
    <td>Загружает документ заново.</td>
  </tr>
  <tr>
    <td>assign()</td>
    <td>Загружает новый документ в том же окне браузера.</td>
  </tr>
</table>
```js
location.assign("http://ya.ru/")  // перенаправит на эту страницу
location.href = "http://ya.ru/"   // перенаправит на эту страницу
location.reload()                 // перезагрузка старницы
location.replace("http://ya.ru/") // нельзя вернутся назад как в assign
```

<h2>History</h2>
<p>
  Объект <strong>History</strong> содержит список URL которые были посещены в данном окне браузера. С помощью свойства <strong>length</strong> Вы можете узнать количество посещенных URL хранящихся в списке.
</p>
<h3>Методы</h3>
<table>
  <tr>
    <th>Метод</th>
    <th>Описание</th>
  </tr>
  <tr>
    <td>back()</td>
    <td>Загружает предыдущий URL (если он есть)</td>
  </tr>
  <tr>
    <td>forward()</td>
    <td>Загружает следующий URL (если была нажата кнопка “назад”)</td>
  </tr>
  <tr>
    <td>go()</td>
    <td>Переходит на указанный URL по его <strong>НОМЕРУ</strong> в списке посещенных страниц. Число указывает смещение относительно текущей URL в списке. Данный параметр может принимать отрицательные значения.</td>
  </tr>
  <tr>
    <td>length</td>
    <td>Сколько переходов сохранено в истории</td>
  </tr>
</table>

<p>Так же, у <strong>history</strong> имеется специальный набор методов, для сохранения произвольных <strong>состояний</strong>. Данный набор методов является частью <strong>HTML 5 API</strong> и будет рассмотрен далее.</p>
