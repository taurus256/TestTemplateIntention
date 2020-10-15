Это Intention для IDEA, предназначенный для генерации шаблонов тестов контроллеров REST API. Не предназначен для генерации законченных тестов (хотя может в простейших случаях)
Может быть вызван для методов с аннотациями @GetMapping, @PostMapping и @PutMapping
# Что делает
 - Формирует вызов mockMvc.perform() с указанием типа(get/post/put) и параметров запроса; параметры запроса инициализируются с помощью 'new ТипПеременной()'
 - Если у метода входной параметр имеет аннотацию @RequestBody, добавляет проверку contentType() при отправке запроса
 - Если у метода значение выходного параметра отлично от ResponseEntity.ok().build(), добавляет проверку contentType() для ответа
 - Пытается сгенерировать моки для всех методов, значение которых присваивается переменным (если значение не присваивается - оно не оказывает влияния на результат и мокировать такой метод не нужно), указывая им 'new ТипПеременной()' как возвращаемое значение в thenReturn(). Это - "бонус",  может пропускать методы или генерить некорректные возвращаемые значения, типа new List().
 # Как установить
1. Сначала нужно открыть настройки (File | Settings | Appearance & Behavior | Path Variables) и внести переменную с именем Method в Ignored Variables. Идея путает переменные скриптов с переменными окружения, если этого не сделать, будет ругаться при старте проекта.
![alt](https://github.com/taurus256/TestTemplateIntention/blob/main/imgs/1.png)
2. Поместить файл Project_Default.xml в папку .idea/inspectionProfiles/ нужного проекта. Если такой папки нет - создать её.
3. Рестартовать Идею, открыть File | Settings | Editor | Inspections и убедиться, что нужная инспекция активна
![alt](https://github.com/taurus256/TestTemplateIntention/blob/main/imgs/2.png)

После этого можно её вызывать с помощью Alt+Enter на аннотации любого REST-метода
 
