# Bounce-game
An independently developed computer game with just one level, its more like a custom version of the bounce computer game

package Game.org;

import java.awt.*
;
import javax.swing.*;
import javax.swing.Timer;
import static javax.swing.JOptionPane.*;
import java.util.*;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.awt.event.WindowEvent;
import java.awt.Color;
import java.awt.Graphics;
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;


public class Bounce extends JFrame implements ActionListener, KeyListener {
	
	Timer t = new Timer(7, this);
	int x =10, velx=0, y=65, vely =1; //for shape size
    int ball_w=30, ball_h=30;
     int value;
     boolean flag;
     boolean live;
     int call =0;
     int ex=885, evx=5, evy;
     static JOptionPane box;
     int k =0;
     int output;
     Bounce fr;
     static int window;
     /*f-> for flying box*/
     int fx =490, fy=530, fvx =1, fvy =0;
     String message = "YOU'VE BEEN ELIMINATED !!!";
     String title = "GAME OVER !";
     
  public Bounce(){
	  
	super("Bounce");
	setLayout(null);
	setSize(1000, 600);
	flag =false;
	live = false;
	addKeyListener(this);
	setFocusable(true);
	
	setFocusTraversalKeysEnabled(false); // this disables other keys(shift) on the keyboard apart from arrow keys
	getContentPane().setBackground(Color.green);
	
	setVisible(true);
	
	
}
  
  public void actionPerformed(ActionEvent e) {
	    
	  /*for the rolling ball*/
	  x = x + velx;
	  y = y + vely;
	  int alt = 0;
	
	  /*for the red moving box*/
	  if(call == 1){
	  fx = fx + fvx;
	  }
	  System.out.println(" " + x + " " + y);
	  
	  /*to make the ball bounce off the top corners*/
	  if(y < 0){
	  vely = - vely;	  
	  }
	  else if(y > 545 && k == 0){ /*if the ball hits the sharp edges*/
		  output = showConfirmDialog(null, "OOps!: Dead End", title, JOptionPane.CLOSED_OPTION);
		  
		  if(output == 0){ 
		  		WindowEvent closingEvent = new WindowEvent(this, WindowEvent.WINDOW_CLOSING);
		  		Toolkit.getDefaultToolkit().getSystemEventQueue().postEvent(closingEvent);
		  		System.exit(0);
		  	}
	  }
	  else if(y >= 495){
		call = 1;  
	  }
	  
	  ex = ex -evx;
	  
	  if(ex < 0 || ex > 950){
		evx = - evx;  
	  }
	  else if((x > ex)){
		  if((y >= 39 && y<=90) || (y>=111 && y<= 150) || (y>=284 && y<=330) || y>=368 && y<=410){
			  
		  output = showConfirmDialog(null, message, title, JOptionPane.CLOSED_OPTION);
		  
		  	if(output == 0){ 
		  		WindowEvent closingEvent = new WindowEvent(this, WindowEvent.WINDOW_CLOSING);
		  		Toolkit.getDefaultToolkit().getSystemEventQueue().postEvent(closingEvent);
		  		System.exit(0);
		  	}
		  	
	  }
	 }	  
	  
	  
	  if(x >=920){
		  if(y >=530){
		  output = showConfirmDialog(null, "Great Work: You made it!\n"
				  + "1000pts!!", "Congratulations", JOptionPane.CLOSED_OPTION);
		  
		  	if(output == 0){ 
		  		WindowEvent closingEvent = new WindowEvent(this, WindowEvent.WINDOW_CLOSING);
		  		Toolkit.getDefaultToolkit().getSystemEventQueue().postEvent(closingEvent);
		  		System.exit(0);
		  	}
		  } 	
	  } 	
	  
	  /*when the ball is inside the house*/
	  if(x > 960){
	  velx = -velx;
	  }
	  else if(x >=842){
		 k = 1;	  /*disable the sharp edge reactions*/
	  }
	  
	  
		  if(fx < 0)
		  fvx = -fvx;	 
		  else if(fx > 800){
		  fvx = -fvx;
		  alt =1;
		  }
		  else{
		  alt =0;	  
		  }
	  	  
	  
	  if(x > 840 && x < 1000){
		flag = true;
		//velx = -velx;
	 }
	 else{
		flag = false; 
	 }
	 
	  if(flag == false){
		 if(y >=495 && (alt == 0)){ 
			// y = 495;
			vely = 0;
			 velx = fvx;
		 }
	  }
    
	  

	 
	  /*to make the ball bounce*/
	  if((y< 12 || y > 65) && x < 341){
		vely = -vely;
	  }
	  else if( y == 145 && x > 554 ){
		  vely= -vely; 
	  }
	  else if( y == 195 && x < 427 )
	  vely= -vely;
	  else if( y == 329 && x > 525 )
		  vely= -vely;
	   repaint();
	   
	 if(x == 589){
		live = true; 
	 }
	   
	}
  
    
	public void paint(Graphics g){
		super.paint(g);
		
	//g.drawArc(bound_x, bound_y, w_width, w_height, -90, 90);
	g.drawRect(10, 100, 340, 20);
	g.setColor(Color.gray);
	g.fillRect(10,  100, 340, 20);
	
	g.drawRect(590, 180, 400, 20);
	g.setColor(Color.cyan);
	g.fillRect(590, 180, 400, 20);
	
	g.drawRect(10, 230, 427, 20);
	g.setColor(Color.magenta);
	g.fillRect(10, 230, 427, 20);
	
	g.drawRect(560, 364, 430, 20);
	g.setColor(Color.blue);
	g.fillRect(560, 364, 430, 20);
     
	g.drawRect(10, 445, 445, 20);
	g.setColor(Color.yellow);
	g.fillRect(10, 445, 445, 20);
	 
	g.drawRect(870, 450, 200, 150);
	g.setColor(Color.black);
	g.fillRect(870, 450, 200, 150);
	
	g.drawRect(920, 540, 40, 59);
	g.setColor(Color.white);
	g.fillRect(920, 540, 40, 59);
	
	
	  
	
	
	

	//the bounce ball
	g.setColor(Color.red);
	g.drawOval(x, y, ball_w, ball_h);
	g.fillOval(x, y, ball_w, ball_h);
	//g.fillOval(x, y, ball_w, ball_h);
	
	 
	
	/*torns of fire on base level*/
	for(int i=10; i<=820; i+=20){
	g.drawOval(i, (580), 20, 40);
	g.setColor(Color.orange);
	g.fillOval(i, (580), 20, 40);
	}
	
	
	
	
	
	g.drawOval(ex, 69, 50, 20);
	g.setColor(Color.black);
	g.fillOval(ex, 69, 50, 20);
		
	g.drawOval(ex, 150, 50, 20);
	g.setColor(Color.black);
	g.fillOval(ex, 150, 50, 20);

	g.drawOval(ex, 320, 50, 20);
	g.setColor(Color.black);
	g.fillOval(ex, 320, 50, 20);
	
	g.drawOval(ex, 400, 50, 20);
	g.setColor(Color.black);
	g.fillOval(ex, 400, 50, 20);
	
	

	
	
	
	
	/*obstacles on the way/bumps*/
	
	g.setColor(Color.black);
	g.drawRect(fx, 530, 55, 40);
	g.fillRect(fx, 530, 55, 40);
	t.start();
	//*/
	
	/*g.drawOval(340, 50, 20, 20);
	g.setColor(Color.yellow);
	g.fillOval(340, 50, 20, 20);*/

	}
	
	@Override
	public void keyPressed(KeyEvent e) {
	int c = e.getKeyCode();
	
	 if(c == KeyEvent.VK_LEFT){
		 velx = -1;
		 vely = 0;
	 }
	 if(c == KeyEvent.VK_UP){
		 velx=0;
		 vely=-1;
	 }
	 if(c == KeyEvent.VK_RIGHT){
		 velx = 1;
		 vely = 0;
	 }
	 if(c == KeyEvent.VK_DOWN){
		  velx =0;
		  vely=1;
	 }
	
	}

	@Override
	public void keyReleased(KeyEvent e) {
		// TODO Auto-generated method stub
		velx = 0;
		if(call == 1)
		 vely =0;
	}

	@Override
	public void keyTyped(KeyEvent e) {
		// TODO Auto-generated method stub
		
	}
	
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		String msg = " try to dodge the black flying daggers\n"
				+ "try to get to the red box beneath the screen\n"
				+ "and then jump ahead to the house in black\n "
				+ "You cannot move vertically behind the horizontal flying daggers,\n"
				+ "i.e you can only move vertically when the daggers are to the right\n"
				+ "of the screen,  Good Luck.\n\n"
				+ " " + " " + " " + " " + " "+ " "+ " "+ " "+ " "+ " " + " " + " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " "+ " " + " " + " " + " "+ " " + " " + "Loading.........\n";
		showMessageDialog(null, msg, "Game Instructions", JOptionPane.INFORMATION_MESSAGE);
      Bounce frame = new Bounce();

	
 }

	
	

}


