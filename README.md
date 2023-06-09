# NLP2
Организовать доступ к модели при помощи REST API    

## Поднятие сервера и получение доступа к нему
После поднятия REST сервера с моделью командой <code>python -m deeppavlov riseapi squad_bert -p 5005</code> он будет запущен на 5005 порту хост-машины.

После инициализации модели к ней можно будет обратиться по URL http://127.0.0.1:5005, при условии, что мы находимся в одной сети с хост-машиной.  
Чтобы организовать доступ к модели из разных сетей был использован сервис Ngrok

Если прописать в консоли ngrok:  <code>ngrok.exe http 5005</code>, то ngrok сгенерирует ссылку, перейдя по которой, мы сможем получить доступ к 5005 порту хост-машины через интернет  

## Инструкция
Получить результаты работы модели, используя свой текст и наш сервер с моделью, можно двумя способами:
> 1) Через cmd 
> 2) Используя графическую оболочку   

## Способ 1  
1) Открываем cmd  
2) Отправлять запрос POST мы будем с помощью инструмента curl  
>curl — инструмент для передачи данных с сервера или на него  

**Шаблон запроса POST:**   
<code>curl -X POST "https://3beb-109-202-60-123.eu.ngrok.io/model" -H "accept: application/json" -H "Content-Type: application/json" 
-d "{\\"context_raw\\":[\\"Ваш_текст\\"], \\"question_raw\\":[\\"Вопрос_по_вашему_тексту\\"]}"</code> 
  
 **Пример:**  
Текст: DeepPavlov is a library for NLP and dialog systems.  
Вопрос по тексту: "What is DeepPavlov?"  
  
<code>curl -X POST "https://3beb-109-202-60-123.eu.ngrok.io/model" -H "accept: application/json" -H "Content-Type: application/json" -d "{\\"context_raw\\":[\\"DeepPavlov is a library for NLP and dialog systems.\\"], \\"question_raw\\":[\\"What is DeepPavlov?\\"]}"</code>  
  
**Получим таккой output:**  
![image info](https://github.com/MyasnikovAndrey/deeppavlov-task2/blob/main/pictures/output.png) 
  
**Ответ получился:** <code>a library for NLP and dialog systems</code>  
**Ответ сервера: 200 - все ОК**  
![image info](https://github.com/MyasnikovAndrey/deeppavlov-task2/blob/main/pictures/server_req.png)  

### Попробуем сделать POST запрос внутри модуля .ipynb jupyter notebook и сохранить результат в переменную  
Получим следующий результат (**ФАЙЛ model_request.ipynb**)  
![image info](https://github.com/MyasnikovAndrey/deeppavlov-task2/blob/main/pictures/jupyter2.png)
