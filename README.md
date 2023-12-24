# code51
package yhck; 
class Bank {
    private double balance;

    public Bank(double initialBalance) {
        this.balance = initialBalance;
    }

    public synchronized void deposit(double amount) {
        balance += amount;
        System.out.println("当前账户余额：" + balance);
    }
}

class depositor implements Runnable {
    private Bank bank;
    private int times;

    public depositor(Bank bank, int times) {
        this.bank = bank;
        this.times = times;
    }

    @Override
    public void run() {
        for (int i = 0; i < times; i++) {
            bank.deposit(100);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Bank bank = new Bank(0);  // 初始余额为0  
        Thread t1 = new Thread(new depositor(bank, 3));  // 创建第一个储户线程  
        Thread t2 = new Thread(new depositor(bank, 3));  // 创建第二个储户线程  
        t1.start();  // 启动第一个储户线程  
        t2.start();  // 启动第二个储户线程  
    }
}
