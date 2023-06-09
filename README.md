# Лабораторная работа № 8
##  Протокол Диффи—Хеллмана

Первый алгоритм с открытым ключом был предложен Диффи и Хеллманом в работе 1976 года «Новые направления в криптографии» (Bailey Whitfield Diffie, Martin Edward Hellman, «New directions in cryptography», [Diffie, Hellman 1976]). Данный протокол, который также можно назвать схемой Диффи—Хеллмана, стал первым, позволивший уменьшить требования к каналу связи для установления защищённого соединения без предварительного обмена ключами.

Протокол позволяет двум сторонам создать общий сеансовый ключ используя такой канал связи, который может прослушивать злоумышленник, но в предположении, что последний не может менять содержимое сообщений.

Пусть   — большое простое число,   — примитивный элемент группы  ,  , причём  ,   и   известны заранее. Функцию   считаем однонаправленной, то есть вычисление функции при известном значении аргумента является лёгкой задачей, а её обращение (нахождение аргумента) при известном значении функции — трудной. (Обратную функцию   называют функцией дискретного логарифма. В настоящий момент не существует быстрых способов вычисления такой функции для больших простых  .)

Протокол обмена состоит из следующих действий.

![alt-текст][L8-1G]

[L8-1G]:https://github.com/b00mmer/Lab_8/blob/main/DH.JPG "DH.jpg"


![alt-текст][L8-2G]

[L8-2G]:https://github.com/b00mmer/Lab_8/blob/main/DH1.JPG "DH1.jpg"


Таким способом создан общий секретный сессионный ключ  . За счёт случайного выбора значений   и   в новом сеансе будет получен новый сессионный ключ.

Протокол обеспечивает только генерацию новых сессионных ключей (цель G10). В отсутствие третей доверенной стороны он не обеспечивает ни аутентификацию сторон (цель G1), из-за отсутствия проходов с подтверждением владения ключом отсутствует аутентификация ключа (цель G8). Зато, так как протокол не использует длительные «мастер»-ключи, можно говорить о том, что он обладает свойством совершенной прямой секретности (цель G9).

Протокол можно использовать только с такими каналами связи, в которые не может вмешаться активный криптоаналитик. В противном случае протокол становится уязвим к простой «атаке посередине».


![alt-текст][L8-3G]

[L8-3G]:https://github.com/b00mmer/Lab_8/blob/main/DH_3_1.jpg "DH_3_1.jpg"



![alt-текст][L8-4G]

[L8-4G]:https://github.com/b00mmer/Lab_8/blob/main/DH2.JPG "DH2.jpg"



В результате Алиса и Боб получили новые сессионные ключи, но «защищённый» канал связи установили не с друг с другом, а со злоумышленником, который теперь имеет возможность ретранслировать или изменять все передаваемые сообщения между Алисой и Бобом.

Протокол Диффи—Хеллмана отличается от большей части протоколов распространения ключей из-за того, что не использует другие криптографические примитивы (функции шифрования, электронно-цифровой подписи или хеширования), но сам по себе является в некотором смысле криптографическим примитивом для построения более сложных протоколов. Он обеспечивает генерацию случайного числа в распределённой системе без доверенного центра. Причём ни одна из сторон не может заставить другую сторону использовать старый сессионный ключ, в отличие от, например, протокола Yahalom.

Протокол можно изменить таким образом, чтобы вместо мультипликативной группы простого умножения использовать аддитивную группу сложения точек эллиптической кривой. В этом случае стороны по прежнему будут выбирать некоторые случайные целые числа, но не возводить генератор-число в степень, а умножать генератор-точку на загаданное число.



##  Решение

 Были разработаны два скрипта SERVER.PY и Client.PY по обмену ключами через сокет localhost.
 
 
![alt-текст][L8-5G]

[L8-5G]:https://github.com/b00mmer/Lab_8/blob/main/Svr.JPG "srv.jpg"


![alt-текст][L8-6G]

[L8-6G]:https://github.com/b00mmer/Lab_8/blob/main/Cli.JPG "cli.jpg"






