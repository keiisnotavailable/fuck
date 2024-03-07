# fuck

import javax.swing.*;

import java.awt.*; // frame

import java.awt.event.*; // object functionality

import java.util.*;

import java.text.*;

import javax.swing.Timer;
import javax.swing.text.AttributeSet;
import javax.swing.text.BadLocationException;
import javax.swing.text.Document;
import javax.swing.text.DocumentFilter;
import javax.swing.text.PlainDocument;

public class ATM {

    static int at = 3;

    static double currentBalance = 1000.0; // Initial balance for current account

    static double savingsBalance = 1000.0; // Initial balance for savings account

    static String accountType; // To store the selected account type

    static double transactionAmount;

    static String transactionType;

    public static void main(String[] args) {

        frame1();

    }

    public static void frame1() {

        JFrame frame1 = new JFrame("Sonic Prime Bank");

        frame1.setSize(1200, 785);

        frame1.setResizable(false);

        frame1.setVisible(true);

        frame1.setLocationRelativeTo(null);

        JPanel pn11 = new JPanel();

        pn11.setBackground(Color.BLUE);

        pn11.setLayout(null);

        frame1.add(pn11);

        JLabel lbl1 = new JLabel();

        lbl1.setIcon(new ImageIcon("C:\\Users\\ADMIN\\Downloads\\1.GIF"));

        lbl1.setBounds(0, 0, 1200, 750);

        pn11.add(lbl1);

        JPasswordField password = new JPasswordField();

        password.setBounds(67, 430, 300, 30);

        password.setBackground(Color.WHITE);

        password.setFont(new Font("SansSerif", Font.BOLD, 25));

        password.setHorizontalAlignment(JPasswordField.CENTER);

        lbl1.add(password);

        password.addKeyListener(new KeyAdapter() {

            @Override

            public void keyPressed(KeyEvent k) {

                String val = password.getText();

                int o = val.length();

                if (o >= 6) {

                    JOptionPane.showMessageDialog(null, "6 CHARACTERS ONLY");

                    password.setText("");

                    password.requestFocus();

                }

                if ((k.getKeyChar() >= '0' && k.getKeyChar() <= '9') || k.getKeyChar() == KeyEvent.VK_BACK_SPACE
                        || k.getKeyChar() == KeyEvent.VK_ENTER) {

                    password.setEditable(true);

                } else {

                    password.setEditable(false);

                }

            }

        });

        JButton btn1 = new JButton("ENTER");

        btn1.setBounds(67, 475, 150, 30);

        btn1.setBackground(new Color(0x7EC17A));

        btn1.setFont(new Font("SansSerif", Font.BOLD, 13));

        lbl1.add(btn1);

        ActionListener btnlist1 = (ActionEvent a) -> {

            if (!password.getText().equals("111111")) {

                JOptionPane.showMessageDialog(null, "INCORRECT PIN");

                at--;

                JOptionPane.showMessageDialog(null, "Remaining Attempt: " + at);

                password.setText("");

                password.requestFocus();

                frame1.getRootPane().setDefaultButton(btn1);

                if (at < 1) {

                    JOptionPane.showMessageDialog(null, "YOU HAVE REACHED MAXIMUM ATTEMPT!");

                    System.exit(0);

                }

            } else {

                JOptionPane.showMessageDialog(null, "LOGIN SUCCESSFUL");

                progress();

                frame1.dispose();

            }

        };

        btn1.addActionListener(btnlist1);

        lbl1.add(btn1);

        JButton btn2 = new JButton("CANCEL");

        btn2.setBounds(228, 475, 140, 30);

        btn2.setBackground(new Color(0xE06060));

        btn2.setFont(new Font("SansSerif", Font.BOLD, 13));

        lbl1.add(btn2);

        ActionListener btnlist2 = (ActionEvent a) -> {

            System.exit(0);

        };

        btn2.addActionListener(btnlist2);

        lbl1.add(btn2);

    }

    public static void progress() {
        final JFrame prog = new JFrame("Sonic Prime Bank");
        prog.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        prog.setSize(1200, 785);
        prog.setLayout(null);
        prog.setLocationRelativeTo(null);

        final JLabel load = new JLabel(new ImageIcon("C:\\Users\\ADMIN\\Downloads\\PROGRESS.gif"));
        load.setBounds(0, 0, 1200, 750);

        final JProgressBar bar = new JProgressBar();
        bar.setBounds(20, 500, 750, 20);
        bar.setForeground(new Color(100, 149, 237));
        bar.setBackground(Color.black);
        bar.setStringPainted(true);
        bar.setVisible(false);

        prog.add(bar);
        prog.add(load);

        Timer timer = new Timer(50, new ActionListener() {
            int progressValue = 0;

            @Override
            public void actionPerformed(ActionEvent e) {
                if (progressValue <= 100) {
                    bar.setValue(progressValue);
                    progressValue++;
                } else {
                    ((Timer) e.getSource()).stop();
                    prog.dispose();
                    frame2();
                }
            }
        });
        timer.start();

        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                prog.setVisible(true);
            }
        });
    }

    public static void frame2() {

        JFrame frame2 = new JFrame("Sonic Prime Bank");

        frame2.setSize(1200, 785);

        frame2.setResizable(false);

        frame2.setVisible(true);

        frame2.setLocationRelativeTo(null);

        JPanel pn2 = new JPanel();

        pn2.setBackground(Color.BLUE);

        pn2.setLayout(null);

        frame2.add(pn2);

        JLabel lbl2 = new JLabel();

        lbl2.setIcon(new ImageIcon("C:\\Users\\ADMIN\\Downloads\\2.GIF"));

        lbl2.setBounds(0, 0, 1200, 750);

        pn2.add(lbl2);

        JButton btn3 = new JButton("DEPOSIT");

        btn3.setBounds(220, 554, 152, 30);

        btn3.setFont(new Font("Futura", Font.BOLD, 20));

        btn3.setForeground(Color.WHITE);

        btn3.setBackground(Color.WHITE);

        btn3.setOpaque(false);

        btn3.setBorder(null);

        lbl2.add(btn3);

        btn3.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                transactionType = "Deposit";

                frame3();

                // you should dispose current frame when you want to navigate to another frame
                frame2.dispose();
            }

        });

        JButton btn4 = new JButton("WITHDRAW");

        btn4.setBounds(515, 556, 152, 30);

        btn4.setFont(new Font("Futura", Font.BOLD, 20));

        btn4.setForeground(Color.WHITE);

        btn4.setBackground(Color.WHITE);

        btn4.setOpaque(false);

        btn4.setBorder(null);

        lbl2.add(btn4);

        btn4.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                transactionType = "Withdraw";

                frame3();

                // you should dispose current frame when you want to navigate to another frame
                frame2.dispose();
            }

        });

        JButton btn5 = new JButton("BALANCE");

        btn5.setBounds(812, 554, 152, 30);

        btn5.setFont(new Font("Futura", Font.BOLD, 20));

        btn5.setForeground(Color.WHITE);

        btn5.setBackground(Color.WHITE);

        btn5.setOpaque(false);

        btn5.setBorder(null);

        lbl2.add(btn5);

        btn5.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                transactionType = "Balance";

                frame3();

                // you should dispose current frame when you want to navigate to another frame
                frame2.dispose();
            }

        });

        JButton btn6 = new JButton("Cancel");

        btn6.setBounds(1010, 638, 152, 30);

        btn6.setFont(new Font("Futura", Font.BOLD, 25));

        btn6.setBackground(new Color(0xE06060));

        lbl2.add(btn6);

        btn6.addActionListener((ActionEvent e) -> {

            int choice = JOptionPane.showConfirmDialog(null, "Are you sure you want to cancel?", null,
                    JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE);

            if (choice == JOptionPane.YES_OPTION) {

                frame1();

                // you should dispose current frame when you want to navigate to another frame
                frame2.dispose();

            }
            // dont need to have an else here, if the choice is no, just display the current
            // frame
            // else {

            // frame2();

            // }

        });

    }

    public static void frame3() {

        JFrame frame3 = new JFrame("Sonic Prime Bank");

        frame3.setSize(1200, 785);

        frame3.setResizable(false);

        frame3.setVisible(true);

        frame3.setLocationRelativeTo(null);

        JPanel pn3 = new JPanel();

        pn3.setBackground(Color.BLUE);

        pn3.setLayout(null);

        frame3.add(pn3);

        JLabel lbl3 = new JLabel();

        lbl3.setIcon(new ImageIcon("C:\\Users\\ADMIN\\Downloads\\3.GIF"));

        lbl3.setBounds(0, 0, 1200, 750);

        pn3.add(lbl3);

        // creating object for balance options
        Object[] balanceOptions = { "Show on screen", "Print receipt" };

        JButton btn7 = new JButton("CURRENT");

        btn7.setBounds(58, 100, 305, 80);

        btn7.setBackground(Color.BLACK);

        btn7.setOpaque(false);

        btn7.setBorder(null);

        btn7.setForeground(Color.WHITE);

        btn7.setFont(new Font("Futura", Font.BOLD, 40));

        lbl3.add(btn7);

        btn7.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                accountType = "Current";

                // checking if transactiontype is balance, then show button promt "Show on
                // screen" and "Print receipt"
                if (transactionType == "Balance") {

                    int choice = JOptionPane.showOptionDialog(null, "Please select options", transactionType,
                            JOptionPane.YES_NO_CANCEL_OPTION, JOptionPane.PLAIN_MESSAGE, null, balanceOptions, balanceOptions[0]);

                    if (choice == JOptionPane.YES_OPTION) {
                        Random rand = new Random();
                        int referenceNumber = rand.nextInt(1000000);

                        SimpleDateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy");
                        SimpleDateFormat timeFormat = new SimpleDateFormat("hh:mm a");
                        Date currentDate = new Date();

                        String accountNumber = "XXXXXXXX1234";
                        String date = dateFormat.format(currentDate);
                        String time = timeFormat.format(currentDate);
                        String accountType = "Savings";
                        double transactionAmount = 1000.0;
                        String transactionType = "Deposit";

            
                        String receiptMessage = 
                        "Account Number: " + accountNumber + "\n"
                        + "Reference Number: " + referenceNumber + "\n"        
            	        + "Date: " + date + "\n"
            	        + "Time: " + time + "\n"
            	        + "Account Type: " + "Savings" + "\n"
            	        + "Current Remaining Balance: " + currentBalance + "\n"           	     
            	        + "\n"
            	        + "Thank you for using SPBank!";
           
                        JOptionPane.showMessageDialog(null, receiptMessage, "Receipt", JOptionPane.PLAIN_MESSAGE);

        
                    } else {
                        // it means print receipt, go to frame6
                        frame6(transactionType);
                        
                        // you should dispose current frame when you want to navigate to another frame
                        frame3.dispose();
                    }

                } else {
                    frame4();

                    // you should dispose current frame when you want to navigate to another frame
                    frame3.dispose();
                }
            }

        });
        

        JButton btn8 = new JButton("SAVINGS");

        btn8.setBounds(58, 265, 305, 80);

        btn8.setBackground(Color.BLACK);

        btn8.setOpaque(false);

        btn8.setBorder(null);

        btn8.setForeground(Color.WHITE);

        btn8.setFont(new Font("Futura", Font.BOLD, 40));

        lbl3.add(btn8);

        btn8.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                accountType = "Savings";

                // checking if transactiontype is balance, then show button promt "Show on
                // screen" and "Print receipt"
                if (transactionType == "Balance") {

                    int choice = JOptionPane.showOptionDialog(frame3, "Please select options", transactionType,
                            JOptionPane.YES_NO_OPTION, JOptionPane.PLAIN_MESSAGE, null, balanceOptions,
                            balanceOptions[0]);

                    if (choice == JOptionPane.YES_OPTION) {
                        Random rand = new Random();
                        int referenceNumber = rand.nextInt(1000000);

        
                        SimpleDateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy");
                        SimpleDateFormat timeFormat = new SimpleDateFormat("hh:mm a");
                        Date currentDate = new Date();

                        String accountNumber = "XXXXXXXX1234";
                        String date = dateFormat.format(currentDate);
                        String time = timeFormat.format(currentDate);
                        String accountType = "Savings";
                        double transactionAmount = 1000.0;
                        String transactionType = "Deposit";

        
                        String receiptMessage = 
                            "Account Number: " + accountNumber + "\n"
                            + "Reference Number: " + referenceNumber + "\n"    
                            + "Date: " + date + "\n"
                            + "Time: " + time + "\n"
                            + "Account Type: " + "Savings" + "\n"
                            + "Remaining Balance:"+ savingsBalance + "\n"
                            + "\n"
                            + "Thank you for your using SPBank!";
                        
                         JOptionPane.showMessageDialog(null, receiptMessage, "Receipt", JOptionPane.PLAIN_MESSAGE);
                         

        
                    } else {
                        // it means print receipt, go to frame6
                        frame6(transactionType);
                        
                        // you should dispose current frame when you want to navigate to another frame
                        frame3.dispose();
                    }

                } else {
                    frame4();

                    // you should dispose current frame when you want to navigate to another frame
                    frame3.dispose();
                }
            }

        });
        

        JButton btn9 = new JButton("Back");

        btn9.setBounds(930, 690, 152, 30);

        btn9.setBackground(new Color(0xC3CBCB));

        btn9.setForeground(Color.BLACK);

        btn9.setFont(new Font("Futura", Font.BOLD, 25));

        lbl3.add(btn9);

        btn9.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                frame2();

                // you should dispose current frame when you want to navigate to another frame
                frame3.dispose();
            }

        });

        JButton btn10 = new JButton("Cancel");

        btn10.setBounds(105, 690, 152, 30);

        btn10.setBackground(new Color(0xE06060));

        btn10.setForeground(Color.BLACK);

        btn10.setFont(new Font("Futura", Font.BOLD, 25));

        lbl3.add(btn10);

        btn10.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                int choice = JOptionPane.showConfirmDialog(null, "Are you sure you want to cancel?", null,
                        JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE);

                if (choice == JOptionPane.YES_OPTION) {

                    frame1();

                    // you should dispose current frame when you want to navigate to another frame
                    frame3.dispose();

                }
                // dont need to have an else here, if the choice is no, just display the current
                // frame
                // else {

                // frame3();

                // }

            }

        });

    }

    public static void frame4() {

        JFrame frame4 = new JFrame("Sonic Prime Bank");

        frame4.setSize(1200, 785);

        frame4.setResizable(false);

        frame4.setVisible(true);

        frame4.setLocationRelativeTo(null);

        JPanel pn3 = new JPanel();

        pn3.setBackground(Color.BLUE);

        pn3.setLayout(null);

        frame4.add(pn3);

        JLabel lbl3 = new JLabel();

        lbl3.setIcon(new ImageIcon("C:\\Users\\ADMIN\\Downloads\\4.GIF"));

        lbl3.setBounds(0, 0, 1200, 750);

        pn3.add(lbl3);

        final JButton oneh = new JButton("PHP 100");

        oneh.setBounds(310, 210, 200, 50);

        oneh.setBackground(Color.BLACK);

        oneh.setOpaque(false);

        oneh.setBorder(null);

        oneh.setForeground(Color.WHITE);

        oneh.setFont(new Font("Futura", Font.BOLD, 25));

        oneh.setBackground(Color.WHITE);

        lbl3.add(oneh);

        oneh.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                transactionAmount = 100.0;
                if (transactionType.equals("Withdraw")) {
                    if (transactionAmount > getCurrentBalance()) {
                        JOptionPane.showMessageDialog(null, "Insufficient balance.");
                        return;
                    } else {
                        askReceipt(frame4);

                    }
                } else if (transactionType.equals("Deposit")) {
                    askReceipt(frame4);
                }
            }
        });

        final JButton twoh = new JButton("PHP 200");

        twoh.setBounds(310, 305, 200, 50);

        twoh.setBackground(Color.BLACK);

        twoh.setOpaque(false);

        twoh.setBorder(null);

        twoh.setForeground(Color.WHITE);

        twoh.setFont(new Font("Futura", Font.BOLD, 25));

        twoh.setBackground(Color.WHITE);

        lbl3.add(twoh);

        twoh.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                transactionAmount = 200.0;

                if (transactionType.equals("Withdraw")) {
                    if (transactionAmount > getCurrentBalance()) {
                        JOptionPane.showMessageDialog(null, "Insufficient balance.");
                        return;
                    } else {
                        askReceipt(frame4);

                    }
                } else if (transactionType.equals("Deposit")) {
                    askReceipt(frame4);
                }
            }
        });
        final JButton fiveh = new JButton("PHP 500");

        fiveh.setBounds(310, 400, 200, 50);

        fiveh.setBackground(Color.BLACK);

        fiveh.setOpaque(false);

        fiveh.setBorder(null);

        fiveh.setForeground(Color.WHITE);

        fiveh.setFont(new Font("Futura", Font.BOLD, 25));

        fiveh.setBackground(Color.WHITE);

        lbl3.add(fiveh);

        fiveh.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                transactionAmount = 500.0;

                if (transactionType.equals("Withdraw")) {
                    if (transactionAmount > getCurrentBalance()) {
                        JOptionPane.showMessageDialog(null, "Insufficient balance.");
                        return;
                    } else {
                        askReceipt(frame4);

                    }
                } else if (transactionType.equals("Deposit")) {
                    askReceipt(frame4);
                }
            }
        });
        final JButton onek = new JButton("PHP 1000");

        onek.setBounds(680, 210, 200, 50);

        onek.setBackground(Color.BLACK);

        onek.setOpaque(false);

        onek.setBorder(null);

        onek.setForeground(Color.WHITE);

        onek.setFont(new Font("Futura", Font.BOLD, 25));

        onek.setBackground(Color.WHITE);

        lbl3.add(onek);

        onek.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                transactionAmount = 1000.0;

                if (transactionType.equals("Withdraw")) {
                    if (transactionAmount > getCurrentBalance()) {
                        JOptionPane.showMessageDialog(null, "Insufficient balance.");
                        return;
                    } else {
                        askReceipt(frame4);

                    }
                } else if (transactionType.equals("Deposit")) {
                    askReceipt(frame4);
                }
            }
        });

        final JButton fivek = new JButton("PHP 5000");

        fivek.setBounds(680, 305, 200, 50);

        fivek.setBackground(Color.BLACK);

        fivek.setOpaque(false);

        fivek.setBorder(null);

        fivek.setForeground(Color.WHITE);

        fivek.setFont(new Font("Futura", Font.BOLD, 25));

        fivek.setBackground(Color.WHITE);

        lbl3.add(fivek);

        fivek.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {
                transactionAmount = 5000.0;
                if (transactionType.equals("Withdraw")) {
                    if (transactionAmount > getCurrentBalance()) {
                        JOptionPane.showMessageDialog(null, "Insufficient balance.");
                        return;
                    } else {
                        askReceipt(frame4);

                    }
                } else if (transactionType.equals("Deposit")) {
                    askReceipt(frame4);
                }
            }
        });

        final JButton tenk = new JButton("PHP 10,000");

        tenk.setBounds(680, 400, 200, 50);

        tenk.setBackground(Color.BLACK);

        tenk.setOpaque(false);

        tenk.setBorder(null);

        tenk.setForeground(Color.WHITE);

        tenk.setFont(new Font("Futura", Font.BOLD, 25));

        tenk.setBackground(Color.WHITE);

        lbl3.add(tenk);

        tenk.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {
                transactionAmount = 10000.0;
                if (transactionType.equals("Withdraw")) {
                    if (transactionAmount > getCurrentBalance()) {
                        JOptionPane.showMessageDialog(null, "Insufficient balance.");
                        return;
                    } else {
                        askReceipt(frame4);

                    }
                } else if (transactionType.equals("Deposit")) {
                    askReceipt(frame4);
                }
            }
        });

        JButton btn11 = new JButton("Back");

        btn11.setBounds(940, 690, 152, 30);

        btn11.setBackground(new Color(0xC3CBCB));

        btn11.setForeground(Color.BLACK);

        btn11.setFont(new Font("Futura", Font.BOLD, 25));

        lbl3.add(btn11);

        btn11.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent t) {

                frame3();

                // you should dispose current frame when you want to navigate to another frame
                frame4.dispose();
            }

        });

        final JButton otheramount = new JButton("Other Amount");

        otheramount.setBounds(400, 560, 410, 50);

        otheramount.setBackground(Color.BLACK);

        otheramount.setOpaque(false);

        otheramount.setBorder(null);

        otheramount.setForeground(Color.WHITE);

        otheramount.setFont(new Font("Futura", Font.BOLD, 25));

        otheramount.setBackground(Color.WHITE);

        lbl3.add(otheramount);

        otheramount.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                frame5();

                frame4.dispose();

            }

        });

        final JButton cancel4 = new JButton("Cancel");

        cancel4.setBounds(130, 690, 152, 30);

        cancel4.setFont(new Font("Futura", Font.BOLD, 25));

        cancel4.setBackground(new Color(0xE06060));

        lbl3.add(cancel4);

        cancel4.addActionListener(new ActionListener() {

            @Override

            public void actionPerformed(ActionEvent e) {

                int choice = JOptionPane.showConfirmDialog(null, "Are you sure you want to cancel?", null,
                        JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE);

                if (choice == JOptionPane.YES_OPTION) {

                    frame1();

                    frame4.dispose();

                }
                // dont need to have an else here, if the choice is no, just display the current
                // frame
                // else {

                // frame4();

                // }

            }

        });

    }

    private static void askReceipt(JFrame jFrame) {

        int choice = JOptionPane.showConfirmDialog(null, "Do you want to print a receipt?", null,
                JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE);
        if (choice == JOptionPane.YES_OPTION) {
            frame6(transactionType);

            // you should dispose current frame when you want to navigate to another frame
            jFrame.dispose();
        } else {
            frame4();
        }
    }

    public static void frame6(String transactionType) {

        Random rand = new Random();
        int referenceNumber = rand.nextInt(1000000);

        SimpleDateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy");
        SimpleDateFormat timeFormat = new SimpleDateFormat("hh:mm a");
        Date currentDate = new Date();

        // change frame1 to frame6 to void confusion
        JFrame frame6 = new JFrame("Sonic Prime Bank");
        frame6.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame6.setSize(1200, 785);
        frame6.setResizable(false);
        frame6.setVisible(true);
        frame6.setLocationRelativeTo(null);

        JPanel pn11 = new JPanel();
        pn11.setBackground(Color.BLUE);
        pn11.setLayout(null);
        frame6.add(pn11);

        JLabel lbl1 = new JLabel();
        lbl1.setIcon(new ImageIcon("C:\\Users\\ADMIN\\Downloads\\6.GIF"));
        lbl1.setBounds(0, 0, 1200, 750);
        pn11.add(lbl1);

        JPanel pn111 = new JPanel();
        pn111.setBackground(Color.BLACK);
        pn111.setBounds(465, 360, 277, 390);
        pn111.setLayout(null);
        lbl1.add(pn111);

        JLabel accNumberLabel = new JLabel("Account Number: XXXXXXX1234");
        accNumberLabel.setFont(new Font("Arial", Font.BOLD, 15));
        accNumberLabel.setBounds(8, 10, 277, 30);
        accNumberLabel.setForeground(Color.WHITE);
        pn111.add(accNumberLabel);
        JLabel dateLabel = new JLabel("Date: " + dateFormat.format(currentDate));
        dateLabel.setFont(new Font("Arial", Font.BOLD, 15));
        dateLabel.setBounds(8, 25, 350, 30);
        dateLabel.setForeground(Color.WHITE);
        pn111.add(dateLabel);

        JLabel timeLabel = new JLabel("Time: " + timeFormat.format(currentDate));
        timeLabel.setFont(new Font("Arial", Font.BOLD, 15));
        timeLabel.setBounds(8, 40, 450, 30);
        timeLabel.setForeground(Color.WHITE);
        pn111.add(timeLabel);

        JLabel accountTypeLabel = new JLabel("Account Type: " + accountType);
        accountTypeLabel.setFont(new Font("Arial", Font.BOLD, 15));
        accountTypeLabel.setBounds(8, 55, 550, 30);
        accountTypeLabel.setForeground(Color.WHITE);
        pn111.add(accountTypeLabel);

        JLabel amountLabel = new JLabel(transactionType + " Amount: PHP " + String.format("%.2f", transactionAmount));
        amountLabel.setFont(new Font("Arial", Font.BOLD, 15));
        amountLabel.setBounds(8, 70, 650, 30);
        amountLabel.setForeground(Color.WHITE);
        pn111.add(amountLabel);

        // balance based on transaction type

        if (accountType.equals("Current")) {

            if (transactionType.equals("Withdraw")) {

                currentBalance -= transactionAmount;

            } else if (transactionType.equals("Deposit")) {

                currentBalance += transactionAmount;

            }

        } else if (accountType.equals("Savings")) {

            if (transactionType.equals("Withdraw")) {

                savingsBalance -= transactionAmount;

            } else if (transactionType.equals("Deposit")) {

                savingsBalance += transactionAmount;

            }

        }

        double newBalance = getCurrentBalance(); // Call the method here
        
        JLabel balanceLabel = new JLabel("Remaining Balance: PHP " + String.format("%.2f", newBalance));
        balanceLabel.setFont(new Font("Arial", Font.BOLD, 15));
        balanceLabel.setBounds(8, 85, 277, 30);
        balanceLabel.setForeground(Color.WHITE);
        pn111.add(balanceLabel);
        
        JLabel thankYouLabel = new JLabel("Thank you for banking");
        thankYouLabel.setFont(new Font("Arial", Font.BOLD, 15));
        thankYouLabel.setBounds(8, 100, 290, 30);
        thankYouLabel.setForeground(Color.WHITE);
        pn111.add(thankYouLabel);
        
        JLabel thankYouLabell = new JLabel("with Sonic Prime Bank!");
        thankYouLabell.setFont(new Font("Arial", Font.BOLD, 15));
        thankYouLabell.setBounds(8, 115, 290, 30);
        thankYouLabell.setForeground(Color.WHITE);
        pn111.add(thankYouLabell);
        pn111.setVisible(false);
        
// timer for exit
        
        Timer timer = new Timer(5000, new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                pn111.setVisible(true);
                Timer exitTimer = new Timer(2000, new ActionListener() {
                    @Override
                    public void actionPerformed(ActionEvent e) {
                        if (transactionType.equals("Balance")) {
                            int anotherTransactionChoice = JOptionPane.showConfirmDialog(null,
                                    "Do you want to perform another transaction?", null, JOptionPane.YES_NO_OPTION,
                                    JOptionPane.QUESTION_MESSAGE);

                            if (anotherTransactionChoice == JOptionPane.YES_OPTION) {
                                frame2();
                            } else {
                                frame1();
                            }
                        } else {
                            frame1();
                        }

                        // you should dispose current frame when you want to navigate to another frame
                        frame6.dispose();
                    }
                });
                exitTimer.setRepeats(false);
                exitTimer.start();

            }
        });
        timer.setRepeats(false);
        timer.start();
        // timer for receipt
        Timer receiptTimer = new Timer(5000, new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                pn111.setVisible(true);
                System.exit(0);
            }
        });
        timer.setRepeats(false);
        timer.start();
    }

    private static double getCurrentBalance() {

        return (accountType.equals("Current")) ? currentBalance : savingsBalance;

    }

    public static void frame5() {
        // change cb to frame5 to avoid confusion
        JFrame frame5 = new JFrame("SONIC PRIME BANK");
        frame5.setSize(1200, 785);
        frame5.setResizable(false);
        frame5.setVisible(true);
        frame5.setLocationRelativeTo(null);
        JPanel cbpanel = new JPanel();
        cbpanel.setBackground(Color.BLUE);
        cbpanel.setLayout(null);
        frame5.add(cbpanel);
        JLabel cbbg = new JLabel();
        cbbg.setIcon(new ImageIcon("C:\\Users\\ADMIN\\Downloads\\5.GIF"));
        cbbg.setBounds(0, 0, 1200, 785);
        cbpanel.add(cbbg);
        JTextField otheramount = new JTextField();
        otheramount.setHorizontalAlignment(SwingConstants.CENTER);
        otheramount.setBounds(400, 339, 400, 50);
        otheramount.setFont(new Font("Futura", Font.BOLD, 25));
        otheramount.setBackground(Color.WHITE);

        // reference: using document filter | Implementing a DocumentFilter.
        // implement filter method for int only
        // limiting to 5 digits only, or 4 index only.
        // dont use keylistner to avoid pasting of text.
        PlainDocument doc = (PlainDocument) otheramount.getDocument();
        doc.setDocumentFilter(new MyIntFilter());

        cbbg.add(otheramount);

        JButton enter = new JButton("Enter");
        enter.setBounds(200, 540, 150, 50);
        enter.setFont(new Font("Futura", Font.BOLD, 25));
        enter.setBackground(Color.GREEN);
        cbbg.add(enter);
        enter.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String inputAmountText = otheramount.getText();
                if (inputAmountText.isEmpty()) {
                    JOptionPane.showMessageDialog(null, "Please enter an amount.");
                    return;
                }
                double inputAmount = Double.parseDouble(inputAmountText);
                if (inputAmount < 100) {
                    JOptionPane.showMessageDialog(null, "Minimum amount is 100.");
                    return;
                }
                if (inputAmount > getCurrentBalance()) {
                    JOptionPane.showMessageDialog(null, "Insufficient balance.");
                    return;
                }
                // add condition to check if the denomination is valid
                // use modulo(%) and 100
                // it will check if it is divisible by 100
                // and checking if it is not equals to 0, dont proceed and show dialog "Please
                // enter a valid amount."
                if ((inputAmount % 100) != 0) {
                    JOptionPane.showMessageDialog(null, "Enter an amount divisible by 100.");
                    return;
                }
                int choice = JOptionPane.showConfirmDialog(null, "Do you want to print a receipt?", null,
                        JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE);
                if (choice == JOptionPane.YES_OPTION) {
                    if (accountType.equals("Current")) {
                        if (transactionType.equals("Deposit")) {
                            transactionAmount = inputAmount;
                            frame6("Deposit");
                        } else if (transactionType.equals("Withdraw")) {
                            transactionAmount = inputAmount;
                            frame6("Withdraw");
                        }
                    } else if (accountType.equals("Savings")) {
                        if (transactionType.equals("Deposit")) {
                            transactionAmount = inputAmount;
                            frame6("Deposit");
                        } else if (transactionType.equals("Withdraw")) {
                            transactionAmount = inputAmount;
                            frame6("Withdraw");
                        } else {
                            frame1();
                        }
                    }
                } else if (choice == JOptionPane.NO_OPTION) {
                    frame1();
                }

                // you should dispose current frame when you want to navigate to another frame
                frame5.dispose();
            }
        });
        JButton clear = new JButton("Clear");
        clear.setBounds(500, 540, 150, 50);
        clear.setFont(new Font("Futura", Font.BOLD, 25));
        clear.setBackground(Color.YELLOW);
        cbbg.add(clear);
        clear.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                otheramount.setText("");
            }
        });

        // rename button, it sshould be Back
        JButton cancel = new JButton("Back");
        cancel.setBounds(795, 540, 150, 50);
        cancel.setFont(new Font("Futura", Font.BOLD, 25));
        cbbg.add(cancel);
        cancel.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                // correct this, instead of frame1 shoule be frame4 for back button
                frame4();

                // you should dispose current frame when you want to navigate to another frame
                frame5.dispose();
            }
        });
    }
}

class MyIntFilter extends DocumentFilter {
    @Override
    public void insertString(FilterBypass fb, int offset, String string,
            AttributeSet attr) throws BadLocationException {

        Document doc = fb.getDocument();
        StringBuilder sb = new StringBuilder();
        sb.append(doc.getText(0, doc.getLength()));
        sb.insert(offset, string);

        if (test(sb.toString())) {
            super.insertString(fb, offset, string, attr);
        } else {
            // warn the user and don't allow the insert
        }
    }

    private boolean test(String text) {

        // limiting the length to 5 digits, like 10,000
        if (text.length() > 5) {
            return false;
        }
        if (text.isEmpty()) {
            return true;
        }

        try {
            Integer.parseInt(text);
            return true;
        } catch (NumberFormatException e) {
            return false;
        }
    }

    @Override
    public void replace(FilterBypass fb, int offset, int length, String text,
            AttributeSet attrs) throws BadLocationException {

        Document doc = fb.getDocument();
        StringBuilder sb = new StringBuilder();
        sb.append(doc.getText(0, doc.getLength()));
        sb.replace(offset, offset + length, text);

        if (test(sb.toString())) {
            super.replace(fb, offset, length, text, attrs);
        } else {
            // warn the user and don't allow the insert
        }

    }

    @Override
    public void remove(FilterBypass fb, int offset, int length)
            throws BadLocationException {
        Document doc = fb.getDocument();
        StringBuilder sb = new StringBuilder();
        sb.append(doc.getText(0, doc.getLength()));
        sb.delete(offset, offset + length);

        if (test(sb.toString())) {
            super.remove(fb, offset, length);
        } else {
            // warn the user and don't allow the insert
        }

    }
}
