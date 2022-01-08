# Traffic-Flow-Counter

##	Отчет

###	Условные обозначения и терминология

- E \- кол-во ребер в сети
- V \- кол-во вершин в сети
- f \- пропускная способность сети
- Остаточная пропускная способность ребра = макс. пропускная способномть ребра - использованная пропускная способность
- Увеличивающий путь - такой путь, в котором осаточная пропускна способность ребра не равна 0
- Остаточная сеть - такая сеть, в которой учтены изменения остаточной пропускной способности
- Вспомогательная сеть - такая сеть, в которой все ребра идут вперед и только к стоку 
- Блокирующий поток - совокупность путей, таких что, в любом пути из истока в сток встретится ребро задействованное в блокирующем потоке 

### Алгоритма Форда-Фалкерсона

- Описание алгоритма:
	1. Берется произвольный увеличивающий путь из истока в сток в остаточной сети
	2. В нем ищется ребро с минимальной остаточной пропускной способностью.
	3. Во всех ребрах пути остаточная пропускная спосоность уменьшается на это значение и оно прибавлятеся к результатц.
	5. Если еще есть увеличивающие пути п.1
	
- Временная сложность в худшем случае = O(E^2*V)[^1]

[^1]: Во всех найденных мною источниках, описываетя алгоритм Форда-Фалкерсона без поиска увеличивающих путей, 
поэтому данные об этой временной сложнсти в интернете, скорее всего будут отличаться  
	-  E*V = сложность поиска в ширину
	-  E, т.к в худшем случае все потоки содержат все ребра


###	Алгоритм Эдмондса-Карпа

- Описание алгоритма:
	1. Берется кратчайший увеличивающий путь из истока в сток в остаточной сети 
	Для нахождения кратчайшего пути, при поиске в ширину при нахождении пути,	он сразу записывается (чем длинее путь, тем позднее он будет найден)
	2. В нем ищется ребро с минимальной остаточной пропускной способностью.
	3. Во всех ребрах пути остаточная пропускная спосоность уменьшается на это значение и оно прибавляется к результату.
	4. Берется новый путь такой, что по нему можно пустить поток (п.1)
	5. Если еще есть увеличивающие пути п.1
	
- Временная сложность в худшем случае такая же, как в алгоритме Ф-Ф = O(E^2*V)[^1]

[^2]: <https://icmmg.nsc.ru/sites/default/files/pubs/om2014-3.pdf>
	-  E*V = сложность поиска в ширину
	-  E, т.к в худшем случае все потоки содержат все ребра

###	Алгоритм Ефима-Диница

- Описание алгоритма:
	1. На основании остаточной сети сторится вспомогательная сеть
	2. Во вспомогательной сети поиском в глубину ищется блокирующий поток
	3. По блокирующему потоку пускается макисмальный возможный поток и он прибавляется к результату
	4. Если еще есть блокирующие потоки п.2
- Временная сложность в худшем случае = O(E*V^2)[^2]

[^3]: <https://e-maxx.ru/algo/dinic>
	-  E*V = сложность поиска блокирующего потока
	-  V, т.к. всего будет V повторений


###	Результаты сравнения

Были произведены 100 запусков программы. Генерировалась сеть с примерно 100 вершин, от каждой из которых исходило по 10 ребер. 
Алгоритмы работали со следующими скоростями:

![Время работы](https://github.com/MkSerdyuk/Traffic-Flow-Counter/blob/Ephim-Dinic-Algorithm/RESULTS.png)