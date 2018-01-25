# Trafficlights
INF-homework
public class Main
{
    // Instanzvariablen - ersetzen Sie das folgende Beispiel mit Ihren Variablen

    public Main(String[ ] args)
    {
        Ampel A = new Ampel();

        Kreuzung kreuzung = new Kreuzung();

        kreuzung.start();
    }

}
public class Ampel
{
    // Instanzvariablen - ersetzen Sie das folgende Beispiel mit Ihren Variablen
    boolean red;
    boolean yellow;
    boolean green;
    public int state = 0;
    int delay = 0;

    public Ampel()
    {
        this.red = true;
        this.yellow = false;
        this.green = false;

    }

    public void state(int state)
    {
        if (state == 0){
            delay = 30;
            red = true;
        } else if (state == 1){
            delay = 3;
            red = true;
            yellow = true;
        } else if (state == 2){
            delay = 30;
            green = true;
        } else if (state == 3){
            delay = 3;
            yellow = true;
        }
    }

    public void next_state(){
        if (state == 0){
            state = 1;
        }
        if (state == 1){
            state = 2;
        }
        if (state == 2){
            state = 3;
        }
        if (state == 3){
            state = 0;
        }
        state(state);
    }

    void print(){
        if (state == 0){
            System.out.println("Rot");
        }
        if (state == 1){
            System.out.println("Gelb/Rot");
        }
        if (state == 2){
            System.out.println("Grün");
        }
        if (state == 3){
            System.out.println("Gelb");
        }
    }
}public class Kreuzung extends Thread
{
    private Ampel A1;
    private Ampel A2;
    public Kreuzung()
    {
        A1 = new Ampel();
        A2 = new Ampel();
        A2.next_state();
        A2.next_state();
    }
    public void run()
    {
        timing();
    }
    public void timing(){
        for (int i = 10; i < 13 ; i++) {
            System.out.println(Thread.currentThread().getName()+" "+i);
            try {
                // thread to sleep for 1000 milliseconds
                Thread.sleep(3000);
            } catch (Exception e) {
                System.out.println(e);
            }
            A1.next_state();
            A2.next_state();
            A1.print();
            A2.print();
        }
    }
}
