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

[L8-3G]:https://github.com/b00mmer/Lab_8/blob/main/DH2.JPG "DH2.jpg"




В результате Алиса и Боб получили новые сессионные ключи, но «защищённый» канал связи установили не с друг с другом, а со злоумышленником, который теперь имеет возможность ретранслировать или изменять все передаваемые сообщения между Алисой и Бобом.

Протокол Диффи—Хеллмана отличается от большей части протоколов распространения ключей из-за того, что не использует другие криптографические примитивы (функции шифрования, электронно-цифровой подписи или хеширования), но сам по себе является в некотором смысле криптографическим примитивом для построения более сложных протоколов. Он обеспечивает генерацию случайного числа в распределённой системе без доверенного центра. Причём ни одна из сторон не может заставить другую сторону использовать старый сессионный ключ, в отличие от, например, протокола Yahalom.

Протокол можно изменить таким образом, чтобы вместо мультипликативной группы простого умножения использовать аддитивную группу сложения точек эллиптической кривой. В этом случае стороны по прежнему будут выбирать некоторые случайные целые числа, но не возводить генератор-число в степень, а умножать генератор-точку на загаданное число.



##  Решение

  Для защиты каналов связи между ЦОДами используется шифрование, и, когда речь заходит о защите канала связи, в памяти всплывают протоколы IPsec, ViPNet VPN, SSL, TLS. Эти протоколы используются в VPN-решениях при построении защищенного удаленного доступа пользователей в инфраструктуру компании, к ее ЦОДам и/или к сервисам облачных операторов. Однако, применительно к сценарию защиты каналов связи между основным и резервным ЦОДами, VPN-решения начинают пасовать, так как важнейшим требованием является быстродействие, которое выражается не в пропускной способности средства шифрования, а в задержке, вносимой системой защиты при передаче данных. Например, стандартная задержка в системах защищенного удаленного доступа составляет порядка 100 миллисекунд, а при резервировании сетевых хранилищ данных приемлемой считается задержка менее 20 миллисекунд. Не стоит забывать и про то, что данные между ЦОДами могут передаваться с использованием специализированных протоколов на уровне L2 модели OSI и применение высокоскоростных шифраторов не будет вносить ограничений в работу этих протоколов, в отличие от криптомаршрутизаторов, обеспечивающих обмен только на уровне L3. 

##  Возможности



