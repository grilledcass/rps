package rps;

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.Random;

public class rps {
    private JFrame mainFrame;
    private JFrame playFrame;
    private JFrame helpFrame;
    private JFrame twoPlayFrame;
    private ImageIcon backgroundIcon;
    private ImageIcon helpIcon;
    private ImageIcon RPSIcon;
    private Boolean twoPlayer;
    String firstPlayerChoice = null;
	String secondPlayerChoice = null;

    public rps() {
    	backgroundIcon = new ImageIcon("/Users/camoc/eclipse-workspace/JFrame/src/images/background.jpg");

        mainFrame = new JFrame("Rock Paper Scissors Game");
        mainFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        mainFrame.setSize(800, 600);
        mainFrame.setContentPane(new JLabel(backgroundIcon));

        JButton playButton = new JButton("PLAY");
        JButton twoPlayer = new JButton("2P MODE");
        JButton helpButton = new JButton("HELP");
        JButton quitButton = new JButton("QUIT"); 
        

        playButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                openPlayWindow();
            }
        });

        helpButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                openHelpWindow();
            }
        });

        quitButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                System.exit(0);
            }
        });
        
        twoPlayer.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
            	openTwoPlayWindow();
            }
        });

        mainFrame.setLayout(new FlowLayout());
        mainFrame.add(playButton);
        mainFrame.add(twoPlayer);
        mainFrame.add(helpButton);
        mainFrame.add(quitButton);
        

        mainFrame.setVisible(true);
    }

    private void openPlayWindow() {
    	twoPlayer = false;
    	RPSIcon = new ImageIcon("/Users/camoc/eclipse-workspace/JFrame/src/images/RPS.jpg");
    	
        playFrame = new JFrame("Play RPS");
        playFrame.setContentPane(new JLabel (RPSIcon));
        playFrame.setSize(800, 470);

        JButton rockButton = new JButton("Rock");
        JButton paperButton = new JButton("Paper");
        JButton scissorsButton = new JButton("Scissors");
        JButton backButton = new JButton("BACK");

        rockButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                playRPS("Rock");
            }
        });

        paperButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                playRPS("Paper");
            }
        });

        scissorsButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                playRPS("Scissors");
            }
        });

        backButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                playFrame.dispose();
            }
        });

        playFrame.setLayout(new FlowLayout());
        playFrame.add(rockButton);
        playFrame.add(paperButton);
        playFrame.add(scissorsButton);
        playFrame.add(backButton);

        playFrame.setVisible(true);
    }
    
    private void openTwoPlayWindow() {
    	twoPlayer = true;
    	
    	JButton rockButton = new JButton("Rock");
        JButton paperButton = new JButton("Paper");
        JButton scissorsButton = new JButton("Scissors");
        JButton backButton = new JButton("BACK");
        
        RPSIcon = new ImageIcon("/Users/camoc/eclipse-workspace/JFrame/src/images/RPS2.jpg");
        
        twoPlayFrame = new JFrame("Play RPS (two player)");
        twoPlayFrame.setContentPane(new JLabel (RPSIcon));
        twoPlayFrame.setSize(800, 470);
        
        rockButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                playRPS("Rock");
            }
        });

        paperButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                playRPS("Paper");
            }
        });

        scissorsButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                playRPS("Scissors");
            }
        });

        backButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
            	twoPlayFrame.dispose();
            }
        });
        
        twoPlayFrame.setLayout(new FlowLayout());
        twoPlayFrame.add(rockButton);
        twoPlayFrame.add(paperButton);
        twoPlayFrame.add(scissorsButton);
        twoPlayFrame.add(backButton);

        twoPlayFrame.setVisible(true);
    }

    private void playRPS(String userChoice) {
        if (twoPlayer) {
            if (firstPlayerChoice == null) {
                firstPlayerChoice = userChoice;
            } else if (secondPlayerChoice == null) {
                secondPlayerChoice = userChoice;
            }

            if (firstPlayerChoice != null && secondPlayerChoice != null) {
                String result;
                if (firstPlayerChoice.equals(secondPlayerChoice)) {
                    result = "It's a tie!";
                } else if ((firstPlayerChoice.equals("Rock") && secondPlayerChoice.equals("Scissors")) ||
                        (firstPlayerChoice.equals("Paper") && secondPlayerChoice.equals("Rock")) ||
                        (firstPlayerChoice.equals("Scissors") && secondPlayerChoice.equals("Paper"))) {
                    result = "Player 1 wins!";
                } else {
                    result = "Player 2 wins!";
                }

                JOptionPane.showMessageDialog(twoPlayFrame, "P1 chose: " + firstPlayerChoice + "\nP2 chose: " + secondPlayerChoice + "\n" + result);

                // Reset player choices
                firstPlayerChoice = null;
                secondPlayerChoice = null;
            }
        } else {
            // Single player mode logic
            String[] options = {"Rock", "Paper", "Scissors"};
            Random random = new Random();
            int computerChoiceIndex = random.nextInt(3);
            String computerChoice = options[computerChoiceIndex];

            String result;
            if (userChoice.equals(computerChoice)) {
                result = "It's a tie!";
            } else if ((userChoice.equals("Rock") && computerChoice.equals("Scissors")) ||
                    (userChoice.equals("Paper") && computerChoice.equals("Rock")) ||
                    (userChoice.equals("Scissors") && computerChoice.equals("Paper"))) {
                result = "You win!";
            } else {
                result = "Computer wins!";
            }

            JOptionPane.showMessageDialog(playFrame, "You chose: " + userChoice + "\nComputer chose: " + computerChoice + "\n" + result);
        }
    }

    private void openHelpWindow() {
    	
    	helpIcon = new ImageIcon("/Users/camoc/eclipse-workspace/JFrame/src/images/help.jpg");
    	
        helpFrame = new JFrame("Help");
        helpFrame.setSize(800, 400);
        helpFrame.setContentPane(new JLabel(helpIcon));

        // Create and add your help content here, e.g., a JLabel with instructions

        JButton backButton = new JButton("BACK");

        backButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                helpFrame.dispose();
            }
        });

        

        helpFrame.setLayout(new FlowLayout());
        // Add your help content here
        helpFrame.add(backButton);
        helpFrame.setVisible(true);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new rps();
            }
        });
    }
}
