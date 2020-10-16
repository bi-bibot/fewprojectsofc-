#include <iostream>
#include <conio.h>
using namespace std;
    const int height=16, width=60;
    enum direction{up1, down1, up2, down2};
    direction dir;
    enum choose {turn1, turn2};
    choose turn;
    int ballx=width/2, bally, countdown=25;
    int player1=0, player2=0;
    int table1x=10;
    int table1y=height/2;
    int table2x=50;
    int chance, first=1;
    int table2y=height/2;
    bool gameover, ready=false, winner=true;
    bool counting, change1, wall, getpoint1, getpoint2, rest;
void game_logic()
    {
        if(winner==true)
        {
        ballx=width/2;
        bally=rand()%10;

        }
        if(rest==true)
        {
            if(change1==true)
            {
                bally--;
            }
            else if(change1==false)
            {
                bally++;
            }
        }
        if(ballx==table1x )
        {
            if(table1y==bally){

            if(change1==true)
            {
                if(dir==up1)
                {
                    rest=true;
                    turn=turn2;
                }
                else if(dir==down1)
                {
                    turn=turn2;
                }
            }
            if(change1==false)
            {
                if(dir==down1)
                    {
                        rest=true;
                        turn=turn2;
                    }

                else if(dir==up1)
                {
                    turn=turn2;

                }


            }
            if(rest==true)
            {
                if(dir==up1 || dir==up2)
                {
                    change1=false;
                    rest=false;
                }
                else if(dir==down1|| dir==down2)
                {
                    change1=true;
                    rest=false;
                }
            }


        }

        }
        if(ballx==table2x )
        {
		
        if(table2y==bally )
        {
            if(change1==true)
            {
                if(dir==up2)
                {
                    rest=true;
                    turn=turn1;
                }
                else if(dir==down2)
                {
                    turn=turn1;
                }
            }
            if(change1==false)
            {
                if(dir==up2)
                {
                    turn=turn1;
                }
                else if(dir==down2)
                {
                    turn=turn1;
                    rest=true;
                }
            }
        }
        }

        if(winner==false){
        switch(turn)
        {
        case turn1:

            ballx--;
            if(wall==false)
            {
            change1=true;
            rest=false;
            }

            else if(bally<0)
            {
                change1=true;
                wall=true;

            }
            if(bally==height)
            {
                wall=true;
                change1=false;
            }
            if(change1==true)
            {
                bally++;

            }
            else if(change1==false)
            {
                bally--;

            }

            break;
        case turn2:
            ballx++;

            if(wall==false)
            {
            change1=true;
            rest=false;
            }

            if(bally<0)
            {
                change1=true;
                wall=true;
            }
            if(bally==height)
            {
                wall=true;
                change1=false;
            }
            if(change1==true)
            {
                bally++;
            }
            if(change1==false)
            {
                bally--;
            }


            break;
        }
        }


        if(counting==true)
        {
            countdown--;
        }
        if(ballx<5)
        {
            winner=true;
            turn=turn1;
            getpoint1=true;
        }
        if(ballx>55)
        {
            winner=true;
            turn=turn2;
            getpoint2=true;
        }

        if(winner==true)
        {
        table1x=10;
        table1y=height/2;
        table2x=50;
        table2y=height/2;
        }
        if(getpoint1==true)
        {
            player1+=1;
            getpoint1=false;
        }
        if(getpoint2==true)
        {
            player2+=1;
            getpoint2=false;
        }





    }
 void gamescreen()
    {
        system("cls");
        cout<<"             first to turns 5 points wins!!!"<<endl;
        cout<< "             " <<player1<<"           "<<player2<<endl;
        for(int i=0; i<width-1; i++)
        {
            if(i==0)
            {
                cout<<char(201);
            }
            if(i==width-2)
            {
                cout<<char(187);
            }
            else
            {
                cout<<char(205);
            }
        }
        cout<<endl;
        for(int i=0; i<height; i++)
        {
            for(int j=0; j<width; j++)
            {
                if(j==0)
                {
                    cout<<char(186);
                }
                else if(j==table1x && i==table1y)
                {
                    cout<<char(221);
                }
                else if(j==width/2)
                {

                }


                else if(j==table2x && i==table2y)
                {
                    cout<<char(222);
                }
                else if(j==ballx && i==bally)
                {
                    cout<<"O";
                }
                else

                {


                    cout<<' ';
                }
                if(j==width-1)
                {
                    cout<<char(186);
                }


            }
             cout<<endl;
        }
        for(int i=0; i<width-1; i++)
        {
            if(i==0)
            {
                cout<<char(200);
            }
            if(i==width-2)
            {
                cout<<char(188);
            }
            else
            {
                cout<<char(205);
            }
        }
        cout<<endl;
        if(first==1)
        {
            cout<<"1. to start player 1"<<endl;
            cout<<"2. to start player 2"<<endl;
            if(kbhit())
            {

                switch(_getch())
                {
                case '1':
                    turn=turn1;
                    first=0;

                    break;
                case '2':
                    turn=turn2;
                    first=0;
                    break;
                }
            }
        }


        if(winner==true)
        {
            cout<<"press 'd' or 'k' to start"<<endl;
           if(kbhit())
           {
               switch(_getch())
               {
               case 'd':
                counting=true;
                ready=true;

                break;
               case 'k':
                counting=true;
                ready=true;
                break;
               }
           }

        }
        if(ready==true)
        {
            cout<<"         game in : "<<countdown<<endl;

        }
        if(countdown==0)
        {
            countdown=25;
            counting=false;
            ready=false;
            winner=false;

        }



    }

    void keyboard()
    {
        if(kbhit())
        {
            switch(_getch())
            {
            case 'w':
               dir=up1;

                break;
            case 's':
               dir=down1;

                break;
            case 'u':
                 dir=up2;
                break;
            case 'j':
                dir=down2;
                break;
            case 'q':
                gameover=true;
                break;


            }
            }
    }
    void moving ()
    {
        switch(dir)
        {
        case up1:
             if(table1y==0);
                else
                {
                    table1y--;
                }
                break;
        case down1 :
             if(table1y==height-1);
                else
                {
                    table1y++;
                }
                break;
        case up2:
            if(table2y==0);
                else
                {
                    table2y--;
                }
                break;
        case down2:
             if(table2y==height-1);
                else
                {
                    table2y++;
                }
                break;
        }
    }

int main()
{
    while(gameover==false)
    {
    game_logic();
    gamescreen();
    keyboard();
    moving();

    }

    return 0;
}
