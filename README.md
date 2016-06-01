package com.veridian.main;

import org.lwjgl.LWJGLException;
import org.lwjgl.opengl.Display;
import org.lwjgl.opengl.DisplayMode;
import org.lwjgl.util.glu.GLU;

import static org.lwjgl.opengl.GL11.*;

public class Compoment 
{
	public boolean running = true;
	
	public static int scale = 3;
	public static String title = "Dino Adventure";
	public static int width = 720 / scale;
	public static int height = 480 / scale;
	
	int time = 0;
	
	DisplayMode mode = new DisplayMode(width * scale,height * scale);
	
	public Compoment()
	{
		try {
			Display.setDisplayMode(mode);
			Display.setResizable(true);
			Display.setFullscreen(false);
			Display.setTitle(title);
			Display.create();
			
			iniGL();
		} catch (LWJGLException e)
		{
			e.printStackTrace();
		}
	}
	private void iniGL()
	{
		glMatrixMode(GL_PROJECTION);
		glLoadIdentity();
		GLU.gluOrtho2D(0, width, height, 0);
		glMatrixMode(GL_MODELVIEW);
		glLoadIdentity();
	}
	
	public void start()
	{
		running = true;
		loop();
	}
	public void stop()
	{
		running = false;
	}
	public void exit()
	{
		Display.destroy();
		System.exit(0);
	}
	
	public void loop()
	{
		while(running){
			if(Display.isCloseRequested()) stop();
			Display.update();
			tick();
			render();
		}
		exit();
	}
	public void tick()
	{
		time++;
	}
	
        public void render()
        {
        	int x = 16 + time / 1000;
        	int y = 16 + time / 1000;
        	int size = 16;
			glBegin(GL_QUADS);
			      glColor3f(1.0F,1.0F,0.7F);
			      glVertex2f(x,y);
			      
			      glColor3f(1.0F,1.0F,0.7F);
				glVertex2f(x + size ,y);
				
				glColor3f(1.0F,0.4F,0.7F);
			      glVertex2f(x + size,y +size  );
			      glColor3f(0.8F,0.3F,0.7F);
			      glVertex2f(x,y + size);
			glEnd();
		}
	
	public static void main(String main[])
	{
		
		Compoment main1 = new Compoment();
		
		main1.start();
		
	}
}
