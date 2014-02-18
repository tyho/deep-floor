#include "testApp.h"

GLfloat lightOnePosition[] = {40.0, 40, 100.0, 0.0};
GLfloat lightOneColor[] = {0.09, 0.09, 0.09, 1.9};

GLfloat lightTwoPosition[] = {-40.0, 40, 100.0, 0.0};
GLfloat lightTwoColor[] = {0.09, 0.19, 0.09, 1.9};

//--------------------------------------------------------------
void testApp::setup(){	
	ofBackground(255,255,255);
    ofHideCursor();
	//ofSetBackgroundAuto(false);
	//ofEnableAlphaBlending();
		
	ofSetVerticalSync(true);

    //some model / light stuff
    glEnable (GL_DEPTH_TEST);
    glShadeModel (GL_SMOOTH);
	
	//allow color and lighting at same time
	glColorMaterial(GL_FRONT_AND_BACK, GL_AMBIENT_AND_DIFFUSE);

    /* initialize lighting */
    glLightfv (GL_LIGHT0, GL_POSITION, lightOnePosition);
    glLightfv (GL_LIGHT0, GL_DIFFUSE, lightOneColor);
    glEnable (GL_LIGHT0);
    glLightfv (GL_LIGHT1, GL_POSITION, lightTwoPosition);
    glLightfv (GL_LIGHT1, GL_DIFFUSE, lightTwoColor);
    glEnable (GL_LIGHT1);
    glEnable (GL_LIGHTING);
    glColorMaterial (GL_FRONT_AND_BACK, GL_DIFFUSE);
    glEnable (GL_COLOR_MATERIAL);

	//glDisable(GL_LIGHTING);
	
    //load the grass model - the 3ds and the texture file, when available, need to be in the same folder
    grassModel.loadModel("grass-block.3DS", 20);

    //you can create as many rotations as you want
    //choose which axis you want it to effect
    //you can update these rotations later on
    //grassModel.setRotation(0, 90, 1, 0, 0);
    //grassModel.setRotation(1, 270, 0, 0, 1);
	grassModel.setRotation(0, 90, 1, 0, 0);
    grassModel.setScale(.6, .6, .6);
    grassModel.setPosition(ofGetWidth()/2, ofGetHeight()/2, 0);

}

//--------------------------------------------------------------
void testApp::update(){
    //grassModel.setRotation(1, 270 + ofGetElapsedTimef() * 60, 0, 0, 1);

}

//--------------------------------------------------------------
void testApp::draw(){
	//ofSetColor(255, 255, 255, 50);
	//ofRect(0, 0, ofGetWidth(), ofGetHeight());
	 //fake back wall
//    ofSetColor(20, 20, 20);
//    glBegin(GL_QUADS);
//        glVertex3f(0.0, ofGetHeight(), -600);
//        glVertex3f(ofGetWidth(), ofGetHeight(), -600);
//        glVertex3f(ofGetWidth(), 0, -600);
//        glVertex3f(0, 0, -600);
//    glEnd();

    //fake wall
//    ofSetColor(50, 50, 50);
//    glBegin(GL_QUADS);
//        glVertex3f(0.0, ofGetHeight(), 0);
//        glVertex3f(ofGetWidth(), ofGetHeight(), 0);
//        glVertex3f(ofGetWidth(), ofGetHeight(), -600);
//        glVertex3f(0, ofGetHeight(), -600);
//    glEnd();
	
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	glOrtho(-ofGetWidth()/2, ofGetWidth()/2,     // left and right
			-ofGetHeight()/2, ofGetHeight()/2,     // top and bottom
			 -1000, 1000);    // near and far

	glMatrixMode(GL_MODELVIEW);
	
    //tumble the world with the mouse
    glPushMatrix();

        //draw in middle of the screen
        glTranslatef(ofGetWidth()/2,ofGetHeight()/2,0);
        //tumble according to mouse
        glRotatef(-mouseY,1,0,0);
        glRotatef(mouseX,0,1,0);
        glTranslatef(-ofGetWidth()/2,-ofGetHeight()/2,0);

		ofSetColor(0, 255, 0, 50);
	    grassModel.draw();

    glPopMatrix();

    //ofSetColor(0x000000);
    //ofDrawBitmapString("fps: "+ofToString(ofGetFrameRate(), 2), 10, 15);

}

//--------------------------------------------------------------
void testApp::keyPressed  (int key){ 

}

//--------------------------------------------------------------
void testApp::keyReleased  (int key){ 
}

//--------------------------------------------------------------
void testApp::mouseMoved(int x, int y ){
}

//--------------------------------------------------------------
void testApp::mouseDragged(int x, int y, int button){
}

//--------------------------------------------------------------
void testApp::mousePressed(int x, int y, int button){
}

//--------------------------------------------------------------
void testApp::mouseReleased(int x, int y, int button){

}
