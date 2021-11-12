# SQL 基础语法
| name      | continent | area | population | gdp |
| ----------- | ----------- |----------- |----------- |----------- |
| Afghanistan | Asia | 652230 | 25500100 | 20343000000 |
| Albania | Europe | 28748 | 2831741 | 12960000000 |
| Algeria | Africa | 2381741 | 37100000 | 188681000000 |
| Andorra | Europe | 468 | 78115 | 3712000000 |
| Angola | Africa | 1246700 | 20609294 | 100990000000 |

#### 单表语句查询
1. 顯示德國 Germany 的人口。

SELECT population FROM world WHERE name = 'Germany'

2. 查詢面積為 5,000,000 以上平方公里的國家,對每個國家顯示她的名字和人均國內生產總值(gdp/population)。

select name, gdp/population from world where area > 5000000

3. 顯示“Ireland 愛爾蘭”,“Iceland 冰島”,“Denmark 丹麥”的國家名稱和人口。

select name, population from world where name in ('Ireland', 'Iceland', 'Denmark')

4. 顯示面積為 200,000 及 250,000 之間的國家名稱和該國面積。

SELECT name, area FROM world WHERE area BETWEEN 200000 AND 250000

**strong 这里注意 between and 的用法**

#### 匹配练习
1. 找出以 Y 為開首的國家。

select name from world where name like 'Y%'

**% 为万用字，可以用于字符匹配**

2. 找出以 Y 為結尾的國家。

select name from world where name like '%Y'

3. 找出所有國家,其名字包括字母x。

SELECT name FROM world WHERE name LIKE '%x%'

4. 找出所有國家,其名字以 land 作結尾。

SELECT name FROM world WHERE name LIKE '%land'

5. 找出所有國家,其名字以 C 作開始,ia 作結尾。

SELECT name FROM world WHERE name LIKE 'C%ia'

6. 找出所有國家,其名字以t作第二個字母。

SELECT name FROM world WHERE name LIKE '_t%' ORDER BY name

** _ 也是万用字符，不过只能匹配一个 **

7. 找出所有國家,其名字都有兩個字母 o,被另外兩個字母相隔着。
SELECT name FROM world WHERE name LIKE '%o__o%'

8. 找出所有國家,其名字都是 4 個字母的。

SELECT name FROM world WHERE name LIKE '____'

9. 顯示所有國家名字,其首都是國家名字加上”City”。

SELECT name FROM world WHERE capital like concat(name, '%City')

** concat 可以用来合并两个或以上的字串

10. "Monaco-Ville"是合併國家名字 "Monaco" 和延伸詞"-Ville".
顯示國家名字，及其延伸詞，如首都是國家名字的延伸。

select name, replace(capital, name, '') where capital like concat('%', name, '%') and name != capital

** replace 替换字段中的内容 **

11. 對於南美顯示以百萬計人口，以十億計2位小數GDP。

select name,round(population/1000000,2),round(gdp/1000000000,2) from world where continent = 'South America'

** round 用于保留小数后多少位 **

12. 顯示國家有至少一個萬億元國內生產總值（萬億，也就是12個零）的人均國內生產總值。四捨五入這個值到最接近1000。

顯示萬億元國家的人均國內生產總值，四捨五入到最近的$ 1000。

select name,round(gdp/population,-3) from world where gdp >= 1000000000000

** round 负数为整数部分四舍五入的精度 **

13. 显示 N 开头的国家，并将大洲属性的 Oceania 改为 Australasia

SELECT name, case when continent = 'Oceania' then 'Australasia' else continent end from world WHERE name LIKE 'N%'

** case when xxx = xxx the xxx else xxx end **

14. Caribbean islands starting with 'B' go to North America, other Caribbean islands go to South America

select name, continent, case when continent = 'Caribbean' and name like 'B%' then 'North America' else (case when continent = 'Caribbean' then 'South America' else continent end ) end from world where continent = 'Caribbean'

15. 寻找 1984 年所有的诺贝尔奖获得者，依据奖项和姓名排序， 化学，物理最后

SELECT winner, subject
  FROM nobel
 WHERE yr=1984
 ORDER BY subject IN ('Physics','Chemistry'), subject, winner

 ** subject IN 将结果转换 0，1

#### 表单组合
1. 在阿根廷Argentina 及 澳大利亞 Australia所在的洲份中，列出當中的國家名字 name 及洲分 continent 。按國字名字順序排序

select name, continent from world where continent in (select continent from world where name in ('Argentina', 'Australia')) order by name 

2. 


#### group by && having

1. 显示每个州有多少个国家

SELECT continent, COUNT(name) FROM world GROUP BY continent

2. 列出有至少100百萬(1億)(100,000,000)人口的洲份。

select continent from world group by continent having sum(population) > 100000000

3. 哪些國家的GDP比Europe歐洲的全部國家都要高呢? [只需列出 name 。] (有些國家的記錄中，GDP是NULL，沒有填入資料的。)

select name from world where gdp > all(select gdp from world where continent = 'Europe' and gdp > 0)


4. 在每一個州中找出最大面積的國家，列出洲份 continent, 國家名字 name 及面積 area。 (有些國家的記錄中，AREA是NULL，沒有填入資料的。)

select continent, name from world x where name <= all(select name from world y where x.continent = y.continent) order by continent

5. 找出洲份，當中全部國家都有少於或等於 25000000 人口. 在這些洲份中，列出國家名字name，continent 洲份和population人口。

select name, continent, population from world a 
where 25000000 > all(select population from world b where b.continent = a.continent and population > 0) 

6. 有些國家的人口是同洲份的所有其他國的3倍或以上。列出 國家名字name 和 洲份 continent。

select a.name, a.continent from world a where a.population / 3 >=  all(select population from world b where a.continent = b.continent and b.population > 0 and a.name <> b.name)


