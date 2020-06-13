Втора лабораториска вежба по Софтверско инженерство

Филип Шабаноски, бр. на индекс 173155

Група на код: Ја добив групата на код 6

-Control Flow Graph
![](/image/cfg.jpg)

-Цикломатска комплексност Цикломатската комплексност на овој код е 4, истата ја добив преку формулата E-N+2, каде што Е е бројот на ребра а N ми е број на јазли. Во случајoв P=22 и N=20, па цикломатската комплексност изнесува 4.

-Тест случаи според критериумот Every statement ....

![](/kriteria/pic1.png)

За Every statement критериумот утврдив 6 минимум случаи со кој ги опфатив сите сценарија кој можат да се случат при тестирање на тест кодот од дадената функцијата. Па преку оваа фотографија може да се види сите тест случаи кој сум ги опфатил во критериумот Every statemen.
Со * ги означив оние линии од кодот кој поминуваат при одреден тест случај и нив ги искористив при тестирање на функцијата.

-Тест случаи според критериумот Multiple condtition ....

![](/kriteria/pic2.png)

При Multiple condtition критериумот утврдив дека има 4 парчин аод кодот кој ќе се извршуваат за тој критериум и кој го исполнуваат тој критериум. Така на пример во случајот if (deg >= 0 && deg < 360) имаме случај кога двата дела се исполнети т.е и двете услови се T.
На пример со инпутот 40,-1,20 го исполнува условот и влегува и го извршува се што е во него.За if (min < 0 || min > 59) имаме пример кога имаме точен исказ и неточен исказ како на пример 40,-1,20, потоа инпут за неточен и точен исказ 40,60,20.
Потоа нареден дел ние if (sec < 0 || sec > 59) каде имам инпут 40,50,-5 кој важи за T || F, потоа инпут 40,50,60 ков важи за F || T.
И за на крај последен таков сличај ни е if (min == 0 && sec == 0) за T && T, инпут ми е 360,0,0 и други многу кој можат да го исполнат одреден дел од условите за Multiple condtition. 

-Објаснување на напишаните unit tests 

 private List<Double> createList(Double... element){
        return new ArrayList<Double>(Arrays.asList(element));
    }
    @Test
    void everyStatementAndEveryBranchTest() {
        RuntimeException ex;
        ex=assertThrows(RuntimeException.class,()->LabExample.sumOfPricesGreaterThan(null,5d));
        assertTrue(ex.getMessage().contains("List of prices is not ok"));

        ex=assertThrows(RuntimeException.class,()->LabExample.sumOfPricesGreaterThan(createList(1d,3d,-2d),2d));
        assertTrue(ex.getMessage().contains("Negative price is not allowed"));

        assertEquals(9d,LabExample.sumOfPricesGreaterThan(createList(1d,4d,5d),2d));
    }

    @Test
    void testEveryPath(){
        RuntimeException ex;
        //1,2,3,12
        ex =assertThrows(RuntimeException.class,
                ()->LabExample.sumOfPricesGreaterThan(null,5d));
        assertTrue(ex.getMessage().contains("List of prices is not ok"));
        //1,2,4,5.1,5.2,6,7,12
        ex=assertThrows(RuntimeException.class,
                ()->LabExample.sumOfPricesGreaterThan(createList(-3d,5d),2d));
        assertTrue(ex.getMessage().contains("Negative price is not allowed"));

        //1,2,4,5.1,5.2,11,12 - can't happen

        //1,2,4,5.1,(5.2,6,8,10,5.3,5.2),11,12
        assertEquals(0,LabExample.sumOfPricesGreaterThan(
                createList(2d,3d),5d));

        //1,2,4,5.1,(5.2,6,8,9,10,5.3,5.2),11,12
        assertEquals(5d,LabExample.sumOfPricesGreaterThan(
                createList(2d,3d),1d));
        //mixed

        //1,2,4,5.1,(5.2,6,8,9,10,5.3,5.2)6,7,12
        ex= assertThrows(RuntimeException.class,()->LabExample.sumOfPricesGreaterThan(
                createList(2d,3d,-4d),1d));
        assertTrue(ex.getMessage().contains("Negative price is not allowed"));

        //1,2,4,5.1,(5.2,6,8,10,5.3,5.2)6,7,12
        ex= assertThrows(RuntimeException.class,()->LabExample.sumOfPricesGreaterThan(
                createList(2d,3d,-4d),5d));
        assertTrue(ex.getMessage().contains("Negative price is not allowed"));
        //mixed
        ex= assertThrows(RuntimeException.class,()->LabExample.sumOfPricesGreaterThan(
                createList(2d,4d,-4d),2d));
        assertTrue(ex.getMessage().contains("Negative price is not allowed"));
    }

    @Test
    void multipleConditionsTest(){

       //if (prices==null || prices.isEmpty())
        //T //F

        //F //T

        //F //F
        RuntimeException ex;
        ex=assertThrows(RuntimeException.class,
                ()->LabExample.sumOfPricesGreaterThan(null,5d));
        assertTrue(ex.getMessage().contains("List of prices is not ok"));

        ex=assertThrows(RuntimeException.class,
                ()->LabExample.sumOfPricesGreaterThan(Collections.emptyList(),5d));
        assertTrue(ex.getMessage().contains("List of prices is not ok"));

        assertEquals(5d,LabExample.sumOfPricesGreaterThan(
                createList(2d,3d),1d));
    }
