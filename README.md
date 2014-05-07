TheBall
=======

Предмет на оваа семинарска работа е создавање на апликацијата The Ball. Самата апликација се состои од три едноставни игри Flappy Ball, Fall Ball и Catch Ball. Идејата за првата игра, Flappy Ball, е земена од  добро познатата Андроид верзија на оваа игра, Flappy Bird. Во втората игра, Fall Ball, треба топчето да се движи надолу низ лавиринт од препреки (полици) и што е можно подолго да се игра без да допри на горниот ѕид. Во третата игра, Catch Ball, целта е да се фатат што е можно повеќе од топчињата кои паѓаат.

=======

Почетното мени содржи форма во која што има три копчиња за одбирање на една од игрите која што ќе се игра. 

![Form1](http://i.imgur.com/ulADcqb.png)

При избор на игра се отвара менито на избраната игра. Во мениот на секоја од игрите има копче за почеток на играта (Start Game), копче за преглед на најдобрите играчи (High Scores), копче за помош како се игра избраната игра (How To Play) и копче за исклучување на играта (Exit Game). 

=======

#### FALL BALL
Освен веќе спомнатите копчиња, играта Fall Ball има можност и за одбирање на тежина на играта, односно три нивоа: Easy, Medium и Hard.

![Menu](http://i.imgur.com/48CKDu2.png)

Со притискање на копчето за почеток на играта се отвара нова форма во која што започнува играта. На горниот дел од формата се прикажува освоените поени, кои се зголемуваат секоја секунда за еден плус. Колку подолго се игра играта без губење толку повеќе поени се добиваат. Движењето на топчето и на полиците е направено во следниот код: 

	private void timer1_Tick(object sender, EventArgs e)
        {
            if (!pause)
            {
                if (!ball.endGame())
                {
                    bool polica = true;
                    intervalScore++;
                    if (intervalScore == 50)
                    {
                        intervalScore = 0;
                        Score++;
                    }
                    for (int i = 0; i < shelfList.Count(); i++)
                    {
                        if (i % 2 == 0)
                            shelfList[i].Move(3, heigh, shelfList[i].width, shelfList[i].x);
                        else
                            shelfList[i].Move(3, heigh, width - shelfList[i - 1].width - 50, shelfList[i - 1].width + 50);
                        if (ball.naPolica(shelfList[i]) && polica)
                        {
                            t = i;
                            polica = false;
                            ball.Move(5, width, heigh, left, right, shelfList[i]);
                        }

                    }
                    if (polica)
                    {
                        if (t % 2 != 0)
                            ball.Move(5, width, heigh, left, right, shelfList[t - 1]);
                        else
                            ball.Move(5, width, heigh, left, right, shelfList[t + 1]);

                    }
                    label2.Text = Score.ToString();
                    panel1.Invalidate(kvadrat, true);
                }
                else
                {
                    endGame();
                }
            }
            else
            {
                timer1.Stop();
            }
        }


