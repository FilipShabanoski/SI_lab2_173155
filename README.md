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

    List<Angle> createList(Angle... element){
        return new ArrayList<Angle>(Arrays.asList(element));
    }
    @Test
    void everyStatementTest(){
        RuntimeException ex;
        Angle angle = new Angle(40,60,20);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angle)));
        assertTrue(ex.getMessage().contains("The minutes of the angle are not valid!"));

        Angle angl2 = new Angle(40,40,60);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angl2)));
        assertTrue(ex.getMessage().contains("The seconds of the angle are not valid"));

        Angle angl3 = new Angle(40,40,50);
        List<Integer> nova2 = SILab2.function(createList(angl3));
//        int indeks1 = nova2.get(0);
        //assertEquals(146450,indeks1);
        for (Integer x: nova2){
            assertEquals(146450, x);
        }

                Angle angl4 = new Angle(360,0,0);
        List<Integer> nova = SILab2.function(createList(angl4));
//        int indeks2 = nova.get(0);
//            assertEquals(1296000,indeks2);
        for (Integer x: nova){
            assertEquals(1296000, x);
        }


        Angle angle5 = new Angle(360,20,30);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angle5)));
        assertTrue(ex.getMessage().contains("The angle is greater then the maximum"));

        Angle angl6 = new Angle(380,20,30);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angl6)));
        assertTrue(ex.getMessage().contains("The angle is smaller or greater then the minimum"));
    }

    @Test
    void MultipleCondititon(){
//        if (deg >= 0 && deg < 360)
//        T && T
//        T && F
//        F && T
//        if (min < 0 || min > 59)
//        T || F
//        F || T
//        F || F
        RuntimeException ex;
        Angle angle = new Angle(40,-1,20);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angle)));
        assertTrue(ex.getMessage().contains("The minutes of the angle are not valid!"));

        Angle angl2 = new Angle(40,60,20);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angl2)));
        assertTrue(ex.getMessage().contains("The minutes of the angle are not valid!"));

        //        if (sec < 0 || sec > 59)
//        T || F
//        F || T
//        F || F
        Angle angl3 = new Angle(40,50,-5);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angl3)));
        assertTrue(ex.getMessage().contains("The seconds of the angle are not valid"));

        Angle angl4 = new Angle(40,50,60);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angl4)));
        assertTrue(ex.getMessage().contains("The seconds of the angle are not valid"));


//        if (min == 0 && sec == 0)
//        T && T
//        T && F
//        F && T

        Angle angl5 = new Angle(360,0,0);
        List<Integer> nova = SILab2.function(createList(angl5));
        for (Integer x: nova){
            assertEquals(1296000, x);
        }

        Angle angl6 = new Angle(360,0,5);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angl6)));
        assertTrue(ex.getMessage().contains("The angle is greater then the maximum"));

        Angle angl7 = new Angle(360,10,0);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angl7)));
        assertTrue(ex.getMessage().contains("The angle is greater then the maximum"));
    }
Горе ми е прикажан кодот од тест случаевите кој ги тестирав за да увидам дали успешно ми работи се што имам досега сработено.
Кај тест случајот за everyStatement прво од Креирам објект од класата angle со вредност 40,60,20 со кој во RuntimeException со кодот ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angle))); го ставам резултатот од асертот од исклучокот ако се случил во листата од агли и потоа во кодот assertTrue(ex.getMessage().contains("The minutes of the angle are not valid!")); дали ја прикажува оваа порака, ако ја прикажува оваа порака тогаш успешно ќе ни помине тестот кој во мојов случај успешто поминува.
Потоа со парчето код    Angle angl2 = new Angle(40,40,60);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angl2)));
        assertTrue(ex.getMessage().contains("The seconds of the angle are not valid")); исто така права втор тест случај кој го зададов и оваа функционира како претходниот парче код и овој нема да го прикажи резултатот на сумата туку ќе заврши програмата и ќе фрли исклучок. Со парчево код Angle angl3 = new Angle(40,40,50);
        List<Integer> nova2 = SILab2.function(createList(angl3));
        for (Integer x: nova2){
            assertEquals(146450, x);
 } имаме успешто пресметана сума и вратена со вредност 40,40,50 и со assertEquals(146450, x); ја проверувам дали 146450 е еднакво со x т.е со вредностите што ги зададов за овој тест случај кој поминуваат како шо треба и нема да се фрли исклучок туку до крај ќе ја пресмета сумата и ќе ја врати.
 Тој ни е третитот тест случај. Четврт тест случај ни е случај кој исто кој ни враќа сумата од функцијата и ни поминува тест случајот успешто со кодот   Angle angl4 = new Angle(360,0,0);
        List<Integer> nova = SILab2.function(createList(angl4));

        for (Integer x: nova){
            assertEquals(1296000, x);
        }
кој се извршува бидејќи поминува условот за  if (min == 0 && sec == 0) пру вредности 360,0,0.
Пети тест случај ми е прикажан со годот 
        Angle angle5 = new Angle(360,20,30);
        ex=assertThrows(RuntimeException.class,()->SILab2.function(createList(angle5)));
        assertTrue(ex.getMessage().contains("The angle is greater then the maximum"));
        при што при инпутуте 360,20,30  if (min == 0 && sec == 0) паѓа условот и оди во else
        каде ќе фрли исклучок ако пораката е The angle is greater then the maximum и успешно ни е поминат тест случајот.
 
