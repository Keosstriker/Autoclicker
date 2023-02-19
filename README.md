using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Runtime.CompilerServices;
using System.Runtime.InteropServices;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Windows.Input;

namespace autoclicker
{
    public partial class Form1 : Form
    {
        int Interval_speed;
        int timeInSec;
        bool IsPause;
        
        public Form1()
        {
            InitializeComponent();
            IsPause = false;
            
        }
        private int Get_Speed()
        {
            
            int speed_Interval=0;
            if(radiobuttonSuperSlow.Checked)
            {
                speed_Interval = 5000;
            }
            if(radioSlow.Checked)
            {
                speed_Interval = 2000;
            }
            if(radioButtonNormal.Checked)
            {
                speed_Interval = 1000;
            }
            if(radioButtonFast.Checked)
            {
                speed_Interval = 500;
            }
            if(radioButtonSuperFast.Checked)
            {
                speed_Interval = 200;
            }
            if(radioButtonUltraFast.Checked)
            {
                speed_Interval = 50;
            }
            if(radioButtonInsanelyFast.Checked)
            {
                speed_Interval= 1;
            }
            return speed_Interval;  

        }//checkSelected Speed
        private int Get_duration()//check Seleted time Duration
        {
            int timeDurationInSec = 0;
            if (radioButton5s.Checked)
            {
                timeDurationInSec= 5;
            }
            if(radioButton10s.Checked)
            {
                timeDurationInSec= 10;  
            }
            if (radioButton30s.Checked)
            {
                timeDurationInSec = 30;
            }
            if (radioButton1min.Checked)
            {
                timeDurationInSec= 60;
            }
            if(radioButton5min.Checked)
            {
                timeDurationInSec = 300;
            }
            if (radioButton10min.Checked)
            {
                timeDurationInSec = 600;
            }
            if(radioButton20min.Checked)
            {
                timeDurationInSec = 1200;
            }
            if(radioButton30min.Checked)
            {
                timeDurationInSec = 1800;
            }
            if(radiobutton40min.Checked)
            {
                timeDurationInSec = 2400;
            }
            if (radioButton50min.Checked)
            {
                timeDurationInSec = 3000;
            }
            if(radioButton1h.Checked)
            {
                timeDurationInSec = 3600;
            }
            if(radioButton8h.Checked)
            {
                timeDurationInSec = 28800;
            }
            if(radioButton12h.Checked)
            {
                timeDurationInSec = 43200;
            }
            if(radioButton24h.Checked)
            {
                timeDurationInSec = 86400;
            }
            return timeDurationInSec;
        }
        [DllImport("user32.dll")]
        

        public static extern void mouse_event(int flags, int x, int Y, int data, int info);
        void Mouse_Click()
        {
            mouse_event((int)Mouseeventflags.leftDown, MousePosition.X, MousePosition.Y, 0, 0);
            mouse_event((int)Mouseeventflags.leftUp, MousePosition.X, MousePosition.Y, 0, 0);         
        }

        
        enum Mouseeventflags
        {
            leftDown=2,
            leftUp=4,           
        };

        private void button_Start_Click(object sender, EventArgs e)
        {
            Interval_speed = Get_Speed();
            timeInSec = Get_duration();
            timer_MouseClick.Interval = Interval_speed;
            timer_MouseClick.Start();
            timerCountSecunds.Start();
            this.Text = "Clicking .....";
            label_remainingTime.Text = timeInSec.ToString();   
        }

        private void timer_MouseClick_Tick(object sender, EventArgs e)
        {
            Mouse_Click();
        }

        private void botton_Stop_Click(object sender, EventArgs e)
        {
            timer_MouseClick.Stop();
            timerCountSecunds.Stop();
            this.Text = "Auto Clicker";
            IsPause = true;
        }

        private void timerCountSecunds_Tick(object sender, EventArgs e)
        {
            if(timeInSec-1>-1)
            {
                timeInSec--;
            }
            
            if(timeInSec < 1)
            {
                timer_MouseClick.Stop();
                timerCountSecunds.Stop();
                this.Text = "Auto Clicker";
            }
            label_remainingTime.Text=timeInSec.ToString();
        }

        private void button_continue_Click(object sender, EventArgs e)
        {
            if(IsPause)
            {
                timer_MouseClick.Start();
                timerCountSecunds.Start();
            }
        }
    }
}

