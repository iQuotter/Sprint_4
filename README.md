### Тестируемый сайт

https://qa-scooter.praktikum-services.ru/

### Задание

    Тестовые сценарии

        Выпадающий список в разделе «Вопросы о важном». Тебе нужно проверить: когда нажимаешь на стрелочку, открывается соответствующий текст. Важно написать отдельный тест на каждый вопрос.
        Заказ самоката. Весь флоу позитивного сценария. Обрати внимание, что есть две точки входа в сценарий: кнопка «Заказать» вверху страницы и внизу.

    Из чего состоит позитивный сценарий:

        Нажать кнопку «Заказать». На странице две кнопки заказа. - реализовано (test_order [@pytest.mark.parametrize('ENTER_BUTTON'...])
        Заполнить форму заказа. - реализовано (enter_order_data, enter_about_rent_date)
        Проверить, что появилось всплывающее окно с сообщением об успешном создании заказа. - реализовано (test_order)
        Проверить: если нажать на логотип «Самоката», попадёшь на главную страницу «Самоката». - реализовано (test_click_on_logo_scooter)
        Проверить: если нажать на логотип Яндекса, в новом окне откроется главная страница Яндекса. - реализовано (test_click_on_logo_yandex)

    Нужно написать тесты с разными данными: минимум два набора. Какие именно данные использовать — на твоё усмотрение. - реализовано через @pytest.mark.parametrize

### Описание

Некоторые локаторы описаны группами например `MODAL_FORM_BUTTONS = (By.XPATH, ".//*[contains(@class, 'Button_Button__ra12g Button_Middle__1CSJM') and text()='Нет'or text()='Да']")`
так как на форме всегда будут кнопки `Да/Нет` \
Или `QUESTIONS_ACCORDION = (By.XPATH, ".//*[contains(@id, 'accordion__heading-')]")` \
В первом случае у нас не так много элементов и не важно как их будут называть, на модальном окне всегда будет две кнопки\
Во втором у нам относительно большой пул однотипных данных и действий, нажали -> сверили текст ответа, вопросов может быть 5, 10, 50, а меняеться у них только индекс

Для `QUESTIONS_ACCORDION` составлен словарь с данными`DICT_ACCORDION_BUTTONS` для сверки ответов

Всего у нас три сценария `test_click_on_question_and_check_answer`-проверка меню "Вопросы о важном", `test_click_on_logo`-клики по кнопкам на логотипе "Яндекс.Самокат", 
`test_order`-позитивный сценарий оформления заказа.\
Все данные для тестов передаются через `@pytest.mark.parametrize`, чтобы не плодить дубли тестов (так же туда можно подтянуть данные из БД)\
В общей сложности они покрывают все задачи и **делают 12 проверок**\

Тест с маркером `@pytest.mark.xfail` падает в браузере Crhome, на модальном окне подтверждения заказа не отрабатывает клик по кнопке `Да`\

| Браузер | Тесты        |
|---------|--------------|
| Firefox | ALL PASSED   |
| Chrome  | 2 TESTS FAIL |