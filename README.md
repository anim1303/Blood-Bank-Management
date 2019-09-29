#include"abhitech.h"
#include<iostream>
#include<conio.h>
#include<fstream>


using namespace std;

class BGroup
{
    public:
        int bgid , qty ;
        char bgroup[3] ;

        void GetBGroup();
        void ShowAll();
        void Showbg();

};

void BGroup::Showbg()
{
    ///Screen();
    BOX(5,35,25,105,14,3);
    int r = 6;
    char str[100];

    sprintf(str,"%-12s %-6d","BG ID       :  ",this->bgid);
    textrc(str,r,37,14,3,0);
    r+= 2;

    sprintf(str,"%-12s %-6s","Blood Group : ",this->bgroup );
    textrc(str,r,37,14,3,0);
    r+=2 ;

    sprintf(str,"%-12s %-6d" , "Quantity  : ",this->qty);
    textrc(str,r,37,14,3,0);


}



     void BGroup::GetBGroup()
     {

       fstream file ;
       char ch ;
       int x,y,n ;
       BGroup bg ;


       file.open("BloodGroup.dat",ios::in|ios::out|ios::binary|ios::ate);

       if(!file)
            file.open("BloodGroup.dat",ios::out|ios::binary);

       n = file.tellp() / sizeof(bg) ;
       cout<<n<<endl ;

       do
       {


          cout<<"\n Enter Bgid ";
          cin>>bg.bgid;

          cout<<"\n Enter Blood Group ";
          cin>>bg.bgroup;

          bg.qty = 0 ;


          file.write(  (char*)&bg ,sizeof(bg) );

          cout<<endl<<"Add more";
          fflush(stdin);
          ch = getche();


       }while(ch=='y' || ch=='Y');


     }


     void BGroup::ShowAll()
     {

              BGroup b;
              char ch;
              char str[50] ;
              int x=0 ,n ;
              fstream file ;
              file.open("BloodGroup.dat",ios::in|ios::out|ios::binary|ios::ate);

              if(!file)
              {
                    Screen();
                    sprintf( str , " No data Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
              }

              else
              {
                 n = file.tellp() / sizeof(b) ;
                 Screen() ;
                 do
                 {

                     file.seekp( (x)*sizeof(b) , ios::beg );
                     file.read( (char*)&b ,sizeof(b)  );
                     b.Showbg();

                     sprintf(str,"%4d OF %4d ",x+1,n);
                     textrc(str,23,90,14,4,0);

                     fflush(stdin) ;
                     ch = _getch() ;

                     if(ch==0 || ch== -32)
                     {
                         ch= _getch() ;

                         if(ch == 80 || ch==77)
                         {
                             x++ ;
                             if(x == n)
                             x = n-1 ;

                         }

                         else if(ch==72 || ch==75)
                         {
                             x-- ;
                             if(x == -1)
                                x = 0 ;
                         }

                     }

                 }while(ch != 27) ;


                 file.close() ;
              }


     }

     class Address
{
    protected:
        char ln1[30];
        char ln2[30];
        char ln3[30];
        char city[30];

    public :
        void getAddress(int &, int);
        void showAddress(int &,int);
        void setempty();

};


void Address::getAddress(int &r,int c)
{
              char str[50];

              sprintf(str,"%-12s" , " Address ");
              textrc(str,r++,c,14,3,0);
              c+=5 ;

              sprintf(str,"%-12s" , " Ln1 : ");
              textrc(str,r++,c,14,3,0);
              fflush(stdin);
              gets(this->ln1);

              sprintf(str,"%-12s" , " Ln2 : ");
              textrc(str,r++,c,14,3,0);
              fflush(stdin);
              gets(this->ln2);

              sprintf(str,"%-12s" , " Ln3 : ");
              textrc(str,r++,c,14,3,0);
              fflush(stdin);
              gets(this->ln3);

              sprintf(str,"%-12s" , " City : ");
              textrc(str,r++,c,14,3,0);
              fflush(stdin);
              gets(this->city);


}

void Address::showAddress(int &r,int c)
{
              char str[50];

              sprintf(str,"%-12s" , " Address ");
              textrc(str,r++,c,14,3,0);
              c+=5 ;

              sprintf(str,"%-12s %-6s" , " Ln1 : ",this->ln1);
              textrc(str,r++,c,14,3,0);

              sprintf(str,"%-12s %-6s" , " Ln2 : ",this->ln2);
              textrc(str,r++,c,14,3,0);

              sprintf(str,"%-12s %-6s" , " Ln3 : ",this->ln3);
              textrc(str,r++,c,14,3,0);

              sprintf(str,"%-12s %-6s" , " City : ",this->city);
              textrc(str,r++,c,14,3,0);


}

void Address::setempty()
{
     ln1[0] = '\0';
     ln2[0] = '\0';
     ln3[0] = '\0';
     city[0]= '\0';
}

struct Date
{
    public:                /// if problem make them private
         int dd,mm,yy ;

    public:
         Date();
         void GetDate(int ,int);
         void ShowDate(int ,int );

};

         Date::Date()
         {
             dd = mm = yy = 0 ;
         }
         void Date::GetDate(int r,int c)
         {
              char str[50];

              sprintf(str, " Day of Month : ");
              textrc(str,++r,c,14,3,0);
              cin>>dd ;

              sprintf(str, "        Month : ");
              textrc(str,++r,c,14,3,0);
              cin>>mm ;

              sprintf(str, "        Year  : ");
              textrc(str,++r,c,14,3,0);
              cin>>yy ;

         }
         void Date::ShowDate(int r,int c)
         {
              char str[50];

              sprintf(str, " %2d/%2d/%4d  ",dd,mm,yy);
              textrc(str,r,c,14,3,0);

         }



     int GenerateBgid(char a[])
     {
            if(strcmp(a,"A+") == 0 )
               return 1;

            else if(strcmp(a,"A-") == 0 )
              return 2;

            else if(strcmp(a,"B+") == 0 )
              return 3;

            else if(strcmp(a,"B-") == 0 )
              return 4;

            else if( strcmp(a,"O+") == 0 )
              return 5;

            else if(strcmp(a,"O-") == 0)
              return 6;

            else if(strcmp(a,"AB+") == 0)
              return 7;

            else if(strcmp(a,"AB-") == 0)
              return 8;

     }




class Donor
{
    public:
        int Did ;
        char Bgroup[4] ;
        int Bgid ;
        char Dnm[50];
        Address addr ;
        char Mob[30];
        Date lddate ;
        int Qty ;

        Donor();
        int GetDonor(int =-1);
        void ShowDonor();
        void setlddate(Date &);

};

void Donor::setlddate(Date &d)
{
    lddate = d ;
}



     Donor::Donor()
     {
         Did = 0;
         Bgroup[0] = '\0' ;
         Bgid = 0;
         Dnm[0] = '\0';
         addr.setempty() ;
         Mob[0] = '\0' ;
         Qty = 0 ;
     }


     int Donor::GetDonor(int x)
     {
              Screen();
              BOX(5,35,25,105,14,3);
              int r  = 6;
              char ch ;
              char str[100];


              sprintf(str,"%-12s %-4d"," DID       : ",this->Did);
              textrc(str,r,37,14,3,0);
              r+= 2;

              sprintf(str,"%-12s",  " Blood Group : " );
              textrc(str,r,37,14,3,0);
              fflush(stdin);
              gets(this->Bgroup);

              Bgid = GenerateBgid(Bgroup) ;
              sprintf(str,"%-12s %-2d" ," Bg ID     : ",Bgid);
              textrc(str,r,60,14,3,0);
              r+= 2;


              if(Bgid<0 || Bgid > 8 )
              {
                 r+=2;
                 sprintf(str,"%-12s"," Enter Correct Bgid ");
                 textrc(str,r,37,14,3,0);
                 fflush(stdin);
                 _getch;
                 return 1 ;

              }


              sprintf(str,"%-12s",     " Donor Name : " );
              textrc(str,r,37,14,3,0);
              fflush(stdin);
              gets(this->Dnm);
              r+=2 ;

              this->addr.getAddress(r,37);
              r++ ;

              sprintf(str,"%-12s",   " Mobile(s)  : " );
              textrc(str,r,37,14,3,0);
              fflush(stdin);
              gets(this->Mob);
              r+=2 ;

              /**

              if(x== -1)
              {
                 sprintf(str,"%-12s", " No of Book(s)   :   0 " );
                 textrc(str,r,37,14,3,0);
                 r+=2 ;

                 sprintf(str,"%-12s  %-4c ", " Status :", 'Y');
                 textrc(str,r,37,14,3,0);
              }

              else
              {
                 sprintf(str,"%-12s", " No of Book(s)   :  " );
                 textrc(str,r,37,14,3,0);
                 fflush(stdin);
                 cin>>this->nobook;
                 r+=2 ;

                 sprintf(str,"%-12s   ", "Status  :  ");
                 textrc(str,r,37,14,3,0);
                 fflush(stdin);
                 ch = getche();
.             }
            */

     }


     void Donor::ShowDonor()
     {

              BOX(5,35,25,105,14,3);
              int r  = 6;
              char str[100];


              sprintf(str,"%-12s %-4d"," DID       : ",this->Did);
              textrc(str,r,37,14,3,0);
              r+= 2;

              sprintf(str,"%-12s %-4s"," Blood Group  : ",this->Bgroup);
              textrc(str,r,37,14,3,0);


              sprintf(str,"%-12s %-4d"," BgId       : ",this->Bgid);
              textrc(str,r,60,14,3,0);
              r+= 2;


              sprintf(str,"%-12s %-6s", " Donor Name   : ",this->Dnm );
              textrc(str,r,37,14,3,0);
              r+=2 ;

              this->addr.showAddress(r,37);
              r++ ;

              sprintf(str,"%-12s %-6s ", " Mobile(s)    : ",this->Mob );
              textrc(str,r,37,14,3,0);
              r+=2 ;

              sprintf(str,"%-12s", " Last Donate Date  : ");
              textrc(str,r,37,14,3,0);
              this->lddate.ShowDate(20,60);
              r+=2 ;


              sprintf(str,"%-12s  %-4d ", " Total QTy Donated :",this->Qty);
              textrc(str,r,37,14,3,0);


     }


     struct DonorFile
     {
         public :
             void EnterDonor();
             void ShowAll();
             void ShowSpecific(int =-1);
             void EditDonor();

      };



      void DonorFile::EnterDonor()
      {
              Donor d ;
              char ch;
              char str[50] ;
              int id ;
              int x ;
              fstream file ;
              file.open("DonorList.dat",ios::in|ios::out|ios::binary|ios::ate);

              if(!file)
                file.open("DonorList.dat",ios::out|ios::binary);



              do
              {
                  id = file.tellp() / sizeof(d) + 1 ;
                  d.Did = id ;    ;

                  x= d.GetDonor() ;

                  if(x==1)
                  {
                      return ;
                  }




                  sprintf(str, "  Save Record (^y/^n) ");
                  textrc(str,21,37,14,3,5) ;
                  fflush(stdin);
                  ch = getche();

                  if(ch=='y' || ch=='Y')
                  {
                     file.write((char *)&d , sizeof(d));
                     sprintf(str, "  Record Added ");
                     textrc(str,22,37,14,3,0) ;
                  }


                  sprintf(str, " Add New Record (^y/^n) ");
                  textrc(str,23,37,14,3,5) ;
                  fflush(stdin) ;
                  ch = getche() ;


              }while(ch=='y' || ch=='Y');

            file.close();

      }

      void DonorFile::ShowAll()
      {
              Donor d ;
              char ch;
              char str[50] ;
              int x=0 ,n ;
              fstream file ;
              file.open("DonorList.dat",ios::in|ios::out|ios::binary|ios::ate);

              if(!file)
              {
                    Screen();
                    sprintf( str , " No data Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
              }


              else
              {

                 n = file.tellp() / sizeof(d) ;
                 Screen();

                 do
                 {

                     file.seekp( (x)*sizeof(d) , ios::beg );
                     file.read( (char*)&d ,sizeof(d)  );
                     d.ShowDonor();

                     sprintf(str,"%4d OF %4d ",x+1,n);
                     textrc(str,23,90,14,4,0);

                     fflush(stdin) ;
                     ch = _getch() ;

                     if(ch==0 || ch== -32)
                     {
                         ch= _getch() ;

                         if(ch == 72 || ch==77)
                         {
                             x++ ;
                             if(x == n)
                             x = n-1 ;
                         }

                         else if(ch==80 || ch==75)
                         {
                             x-- ;
                             if(x == -1)
                                x = 0 ;
                         }

                     }

                 }while(ch != 27) ;


                 file.close() ;
              }

      }

      void DonorFile::ShowSpecific(int x)
      {
              Donor d;
              char ch;
              char str[50] ;
              int n ;
              int y=x ;
              fstream file ;
              file.open("DonorList.dat",ios::in|ios::out|ios::binary|ios::ate);

              if(!file)
              {
                    Screen();
                    sprintf( str , " No data Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
              }

              else
              {
                n = file.tellp() / sizeof(d) ;


                if(x==-1)
                {
                  Screen();
                  BOX(5,35,12,95,11,1);


                  sprintf(str," Total Records Found  %d",n);
                  textrc(str,6,37,14,3,0);

                  sprintf(str," Enter Record no  ");
                  textrc(str,8,37,14,3,0);
                  cin>>x ;
                  x-- ;

                }

                 if(x >= 0 && x< n)
                 {
                     Screen();
                     file.seekp( x*sizeof(d),ios::beg);
                     file.read( (char *)&d , sizeof(d) );
                     d.ShowDonor();
                     if(y==-1)
                     {
                         fflush(stdin);
                         _getch;
                     }

                 }
                 else
                 {
                      sprintf(str," Enter Valid Record no. ");
                      textrc(str,10,37,14,3,0);
                      fflush(stdin);
                      _getch;
                 }

                 file.close();

              }


      }


      void DonorFile::EditDonor()
      {

              Donor d ;
              char ch;
              char str[50] ;
              int n ;
              fstream file ;
              file.open("DonorList.dat",ios::in|ios::out|ios::binary|ios::ate);

              if(!file)
              {
                    Screen();
                    sprintf( str , " No data Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
              }

              else
              {
                  n = file.tellp() / sizeof(d) ;

                  do
                  {
                      Screen();
                      BOX(5,35,24,95,11,1);

                      sprintf(str," Total Records Found  %d",n);
                      textrc(str,6,37,14,3,0);

                      sprintf(str," Enter Record no to be edited  ");
                      textrc(str,8,37,14,3,0);
                      cin>>x ;
                      x-- ;

                     if(x >= 0 && x< n)
                     {

                        file.close();
                        this->ShowSpecific(x);  /// error kare toh iske pehle close karo
                        file.open("DonorList.dat",ios::in|ios::out|ios::binary|ios::ate);

                         sprintf(str, "  Edit Record (^y/^n) ");
                         textrc(str,24,37,14,3,5) ;
                         fflush(stdin);
                         ch = getche();

                         if(ch == 'y' || ch== 'Y')
                         {
                             /// Screen();
                             d.Did = x+1 ;
                             d.GetDonor(x);


                             sprintf(str, "  Save Record (^y/^n) ");
                             textrc(str,21,37,14,3,5) ;
                             fflush(stdin);
                             ch = getche();

                             if(ch=='y' || ch=='Y')
                             {
                                 file.seekp(x*sizeof(d),ios::beg);
                                 file.write( (char *)&d,sizeof(d));
                                 sprintf(str, "  Record Edited ");
                                 textrc(str,22,37,14,3,5) ;

                             }

                         }

                     }
                     else
                     {
                      sprintf(str," Enter Valid Record no. ");
                      textrc(str,10,37,14,3,0);
                      fflush(stdin);
                      _getch;
                     }


                     sprintf(str, "  Edit MOre Records (^y/^n) ");
                     textrc(str,23,37,14,3,5) ;
                     fflush(stdin);
                     ch = getche();


                  }while(ch == 'y' || ch=='Y');


                 file.close();

             }

      }

      class Patient
{
    public:
        int Pid ;
        char Bgroup[4] ;
        int Bgid ;
        char Pnm[50];
        Address addr ;
        char Mob[30];
        Date ltdate ;
        int Qty ;

        Patient();
        int GetPatient(int =-1);
        void ShowPatient();


};


     Patient::Patient()
     {
         Pid = 0;
         Bgroup[0] = '\0' ;
         Bgid = 0;
         Pnm[0] = '\0';
         addr.setempty() ;
         Mob[0] = '\0' ;
         Qty = 0 ;
     }


     int Patient::GetPatient(int x)
     {
              Screen();
              BOX(5,35,25,105,14,3);
              int r  = 6;
              char ch ;
              char str[100];
              int y ;


              sprintf(str,"%-12s %-4d"," Pid       : ",this->Pid);
              textrc(str,r,37,14,3,0);
              r+= 2;

              sprintf(str,"%-12s",  " Blood Group : " );
              textrc(str,r,37,14,3,0);
              fflush(stdin);
              gets(this->Bgroup);

              Bgid = GenerateBgid(Bgroup) ;
              sprintf(str,"%-12s %-2d" ," Bg ID     : ",Bgid);
              textrc(str,r,60,14,3,0);
              r+= 2;

              if(Bgid<0 || Bgid > 8 )
              {
                 r+=2;
                 sprintf(str,"%-12s"," Enter Correct Bgid ");
                 textrc(str,r,37,14,3,0);
                 fflush(stdin);
                 _getch;
                 return 1 ;

              }



              sprintf(str,"%-12s",     " Patient Name : " );
              textrc(str,r,37,14,3,0);
              fflush(stdin);
              gets(this->Pnm);
              r+=2 ;

              this->addr.getAddress(r,37);
              r++ ;

              sprintf(str,"%-12s",   " Mobile(s)  : " );
              textrc(str,r,37,14,3,0);
              fflush(stdin);
              gets(this->Mob);
              r+=2 ;


     }


     void Patient::ShowPatient()
     {
          ///    Screen();
              BOX(5,35,25,105,14,3);
              int r  = 6;
              char str[100];


              sprintf(str,"%-12s %-4d"," Pid       : ",this->Pid);
              textrc(str,r,37,14,3,0);
              r+= 2;

              sprintf(str,"%-12s %-4s"," Blood Group  : ",this->Bgroup);
              textrc(str,r,37,14,3,0);


              sprintf(str,"%-12s %-4d"," BgId       : ",this->Bgid);
              textrc(str,r,60,14,3,0);
              r+= 2;


              sprintf(str,"%-12s %-6s", " Patient Name   : ",this->Pnm );
              textrc(str,r,37,14,3,0);
              r+=2 ;

              this->addr.showAddress(r,37);
              r++ ;

              sprintf(str,"%-12s %-6s ", " Mobile(s)    : ",this->Mob );
              textrc(str,r,37,14,3,0);
              r+=2 ;

              sprintf(str,"%-12s", " Last Taken Date  : ");
              textrc(str,r,37,14,3,0);
              this->ltdate.ShowDate(20,60);
              r+=2 ;


              sprintf(str,"%-12s  %-4d ", " Total QTy Taken :",this->Qty);
              textrc(str,r,37,14,3,0);


     }


     struct PatientFile
     {
         public :
             void EnterPatient();
             void ShowAll();
             void ShowSpecific(int =-1);
             void EditPatient();

      };



      void PatientFile::EnterPatient()
      {
              Patient p ;
              char ch;
              char str[50] ;
              int id ;
              int x ;
              fstream file ;
              file.open("PatientList.dat",ios::in|ios::out|ios::binary|ios::ate);

              if(!file)
                file.open("PatientList.dat",ios::out|ios::binary);



              do
              {
                  id = file.tellp() / sizeof(p) + 1 ;
                  p.Pid = id ;    ;

                  x = p.GetPatient() ;
                  if(x==1)
                  {
                      return ;
                  }



                  sprintf(str, "  Save Record (^y/^n) ");
                  textrc(str,21,37,14,3,5) ;
                  fflush(stdin);
                  ch = getche();

                  if(ch=='y' || ch=='Y')
                  {
                     file.write((char *)&p , sizeof(p));
                     sprintf(str, "  Record Added ");
                     textrc(str,22,37,14,3,0) ;
                  }


                  sprintf(str, " Add New Record (^y/^n) ");
                  textrc(str,23,37,14,3,5) ;
                  fflush(stdin) ;
                  ch = getche() ;


              }while(ch=='y' || ch=='Y');

            file.close();

      }

      void PatientFile::ShowAll()
      {
              Patient p ;
              char ch;
              char str[50] ;
              int x=0 ,n ;
              fstream file ;
              file.open("PatientList.dat",ios::in|ios::out|ios::binary|ios::ate);

              if(!file)
              {
                    Screen();
                    sprintf( str , " No data Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
              }


              else
              {

                 n = file.tellp() / sizeof(p) ;
                 Screen();

                 do
                 {

                     file.seekp( (x)*sizeof(p) , ios::beg );
                     file.read( (char*)&p ,sizeof(p)  );
                     p.ShowPatient();

                     sprintf(str,"%4d OF %4d ",x+1,n);
                     textrc(str,23,90,14,4,0);

                     fflush(stdin) ;
                     ch = _getch() ;

                     if(ch==0 || ch== -32)
                     {
                         ch= _getch() ;

                         if(ch == 72 || ch==77)
                         {
                             x++ ;
                             if(x == n)
                             x = n-1 ;
                         }

                         else if(ch==80 || ch==75)
                         {
                             x-- ;
                             if(x == -1)
                                x = 0 ;
                         }

                     }

                 }while(ch != 27) ;


                 file.close() ;
              }

      }

      void PatientFile::ShowSpecific(int x)
      {
              Patient p;
              char ch;
              char str[50] ;
              int n ;
              int y=x ;
              fstream file ;
              file.open("PatientList.dat",ios::in|ios::out|ios::binary|ios::ate);

              if(!file)
              {
                    Screen();
                    sprintf( str , " No data Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
              }

              else
              {
                n = file.tellp() / sizeof(p) ;


                if(x==-1)
                {
                  Screen();
                  BOX(5,35,12,95,11,1);


                  sprintf(str," Total Records Found  %d",n);
                  textrc(str,6,37,14,3,0);

                  sprintf(str," Enter Record no  ");
                  textrc(str,8,37,14,3,0);
                  cin>>x ;
                  x-- ;

                }

                 if(x >= 0 && x< n)
                 {
                      Screen();
                     file.seekp( x*sizeof(p),ios::beg);
                     file.read( (char *)&p , sizeof(p) );
                     p.ShowPatient();
                     if(y==-1)
                     {
                         fflush(stdin);
                         _getch;
                     }

                 }
                 else
                 {
                      sprintf(str," Enter Valid Record no. ");
                      textrc(str,10,37,14,3,0);
                      fflush(stdin);
                      _getch;
                 }

                 file.close();

              }


      }


      void PatientFile::EditPatient()
      {

              Patient p ;
              char ch;
              char str[50] ;
              int n ;
              fstream file ;
              file.open("PatientList.dat",ios::in|ios::out|ios::binary|ios::ate);

              if(!file)
              {
                    Screen();
                    sprintf( str , " No data Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
              }

              else
              {
                  n = file.tellp() / sizeof(p) ;

                  do
                  {
                      Screen();
                      BOX(5,35,24,95,11,1);

                      sprintf(str," Total Records Found  %d",n);
                      textrc(str,6,37,14,3,0);

                      sprintf(str," Enter Record no to be edited  ");
                      textrc(str,8,37,14,3,0);
                      cin>>x ;
                      x-- ;

                     if(x >= 0 && x< n)
                     {

                         file.close();
                         this->ShowSpecific(x);  /// error kare toh iske pehle close karo
                         file.open("PatientList.dat",ios::in|ios::out|ios::binary|ios::ate);

                         sprintf(str, "  Edit Record (^y/^n) ");
                         textrc(str,24,37,14,3,5) ;
                         fflush(stdin);
                         ch = getche();

                         if(ch == 'y' || ch== 'Y')
                         {
                             /// Screen();
                             p.Pid = x+1 ;
                             p.GetPatient(x);


                             sprintf(str, "  Save Record (^y/^n) ");
                             textrc(str,21,37,14,3,5) ;
                             fflush(stdin);
                             ch = getche();

                             if(ch=='y' || ch=='Y')
                             {
                                 file.seekp(x*sizeof(p),ios::beg);
                                 file.write( (char *)&p,sizeof(p));
                                 sprintf(str, "  Record Edited ");
                                 textrc(str,22,37,14,3,5) ;

                             }

                         }

                     }
                     else
                     {
                      sprintf(str," Enter Valid Record no. ");
                      textrc(str,10,37,14,3,0);
                      fflush(stdin);
                      _getch;
                     }


                     sprintf(str, "  Edit MOre Records (^y/^n) ");
                     textrc(str,23,37,14,3,5) ;
                     fflush(stdin);
                     ch = getche();


                  }while(ch == 'y' || ch=='Y');


                 file.close();

             }

      }
class DonorDetail
{
    public:
        Date Ddate ;
        int Qty ;

        void RecieveBlood();
        void setDdate(Date &);
        void showdd();
        void ShowDetail() ;

};

void DonorDetail::showdd()
{
///    Screen();
    BOX(5,35,25,105,14,3);
    int r = 6;
    char str[100];


    sprintf(str,"%-12s", " Donated Date  : ");
    textrc(str,r,37,14,3,0);
    this->Ddate.ShowDate(6,60);
    r+= 2 ;

    sprintf(str,"%-12s %-6d" , "Quantity  : ",this->Qty);
    textrc(str,r,37,14,3,0);

}

void DonorDetail::ShowDetail()
{
    DonorDetail ddetail ;
    Donor d ;
    DonorFile Df ;
    char ch;
    char str[50] ;
    int n ;
    fstream file ;

    file.open("DonorList.dat",ios::in|ios::out|ios::binary|ios::ate);

                if(!file)
                {
                    Screen();
                    sprintf( str , " No data Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
                }

                else
                {


                    n = file.tellp() / sizeof(d) ;

                      Screen();
                      BOX(5,35,24,95,11,1);

                      sprintf(str," Total Records Found  %d",n);
                      textrc(str,6,37,14,3,0);

                      sprintf(str," Enter Donor Id  ");
                      textrc(str,8,37,14,3,0);
                      cin>>x ;
                      x-- ;

                      if(x >= 0 && x< n)
                      {

                         file.close();
                         Df.ShowSpecific(x);  /// error kare toh iske pehle close karo
                         fflush(stdin);
                         _getch;

                         sprintf(str,"Donor%d.dat",x+1);
                         file.open(str,ios::in|ios::binary|ios::ate);

                         if(!file)
                         {
                              Screen();
                              sprintf(str," No data FOund ");
                              textrc(str,6,37,14,3,0);
                              fflush(stdin);
                              _getch;
                         }

                         else
                         {
                             n = file.tellp() / sizeof(ddetail) ;
                             Screen();

                             do
                             {

                                 file.seekp( (x)*sizeof(ddetail) , ios::beg );
                                 file.read( (char*)&ddetail ,sizeof(ddetail)  );
                                 ddetail.showdd() ;

                                 sprintf(str,"%4d OF %4d ",x+1,n);
                                 textrc(str,23,90,14,4,0);
                                 fflush(stdin) ;
                                 ch = _getch() ;

                                  if(ch==0 || ch== -32)
                                  {
                                        ch= _getch() ;

                                            if(ch == 80 || ch==77)
                                            {
                                                x++ ;
                                                if(x == n)
                                                x = n-1 ;

                                            }

                                            else if(ch==72 || ch==75)
                                            {
                                                x-- ;
                                                if(x == -1)
                                                x = 0 ;
                                            }

                                    }

                             }while(ch != 27);


                         }


                       file.close();

                      }
                      else
                     {
                      file.close();
                      sprintf(str," Enter Valid Donor Id ");
                      textrc(str,10,37,14,3,0);
                      fflush(stdin);
                      _getch;
                     }




                }

}


void DonorDetail::RecieveBlood()
{
    DonorDetail ddetail ;
    char ch,str[50] ;
    Patient p;
    Donor d;
    BGroup b ;
    int totDonor ,dd  ; /// Donor id dd ,


    fstream file,fbg,fp,fd ;

    file.open("DonorList.dat",ios::in|ios::ate|ios::binary);

            if(!file)
            {
                    Screen();
                    sprintf( str , " No Donor Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
                    return ;

            }

            else
            {
                totDonor = file.tellg() / sizeof(d) ;

            }

            file.close();

            fd.open("DonorList.dat",ios::in|ios::out|ios::binary);

            do
            {

                      Screen();
                      BOX(5,35,24,95,11,1);


                      sprintf(str," Enter Donor Id ");
                      textrc(str,6,37,14,3,0);

                      cin>>dd ;
                      dd-- ;


                      if(dd < 0 || dd >= totDonor)
                      {
                          sprintf(str," Enter Valid Donor Id ");
                          textrc(str,8,37,14,3,0);

                          sprintf(str," Take From Other Donor (^Y/^N) ");
                          textrc(str,10,37,14,3,0);
                          fflush(stdin);
                          ch = getche() ;
                          continue ;
                      }


                      fd.seekp( dd*sizeof(d) , ios::beg );
                      fd.read( (char *)&d , sizeof(d) );
                      d.ShowDonor();
                      fflush(stdin);
                      _getch;


       ///                     Screen();
                      BOX(5,35,25,105,11,1);



                      sprintf(str," Enter Donation Date ");
                      textrc(str,7,37,14,3,0);
                      ddetail.Ddate.GetDate(7,41);

                      if( (ddetail.Ddate.dd+ddetail.Ddate.mm*30+ddetail.Ddate.yy*365) - (d.lddate.dd+d.lddate.mm*30+d.lddate.yy*365)  < 90)
                      {
                        sprintf(str," You Cannnot Donate Blood !!! Less than 3 Months ");
                        textrc(str,12,37,14,3,0);

                        sprintf(str," Take From Other Donor (^Y/^N) ");
                        textrc(str,14,37,14,3,0);
                        fflush(stdin);
                        ch = getche() ;
                        continue ;

                      }

                      ddetail.Qty = 1;
                      sprintf(str,"%-12s  %-4d ", "  QTy Donated :",ddetail.Qty);
                      textrc(str,12,37,14,3,0);


                      sprintf(str," Donate Blood (^Y/^N) ");
                      textrc(str,14,37,14,3,0);
                      fflush(stdin);
                      ch = getche();

                      if( ch=='Y' || ch== 'y')
                      {

                        sprintf(str,"Donor%d.dat",d.Did);
                        file.open(str,ios::in|ios::out|ios::binary|ios::ate);

                        if(!file)
                            file.open(str,ios::out|ios::binary);


                        file.write( (char*)&ddetail , sizeof(ddetail));
                        file.close();

                        d.setlddate(ddetail.Ddate);
                        d.Qty += 1 ;

                        d.ShowDonor();
                        fflush(stdin);
                        _getch;

                        fd.seekp( dd*sizeof(d) , ios::beg );
                        fd.write( (char *)&d , sizeof(d) );


                        file.open("BloodGroup.dat",ios::in|ios::out|ios::binary);

                        file.seekp( (d.Bgid-1)*sizeof(b),ios::beg);
                        file.read( (char *)&b , sizeof(b) );
                        b.qty += 1 ;
                        b.Showbg();

                        file.seekp( (d.Bgid-1)*sizeof(b),ios::beg);
                        file.write( (char *)&b , sizeof(b) );

                        file.close();

                        sprintf(str," Data Saved ");
                        textrc(str,16,37,14,3,0);



                      }



                      sprintf(str," Take From Other Donor (^Y/^N) ");
                      textrc(str,18,37,14,3,0);
                      fflush(stdin);
                      ch = getche();



            }while(ch=='y' || ch=='Y');

            fd.close();


}
class PatientDetail
{
    public:
        Date Tdate ;
        int Qty ;

        void ProvideToPatient();
        void ShowDetail();
        void showpd();


};

void PatientDetail::showpd()
{
   /// Screen();
    BOX(5,35,25,105,14,3);
    int r = 6;
    char str[100];


    sprintf(str,"%-12s", " Taken Date : ");
    textrc(str,r,37,14,3,0);
    this->Tdate.ShowDate(6,60);
    r+= 2 ;

    sprintf(str,"%-12s %-6d" , "Quantity  : ",this->Qty);
    textrc(str,r,37,14,3,0);

}

void PatientDetail::ShowDetail()
{
    PatientDetail pdetail ;
    Patient p ;
    PatientFile Pf ;
    char ch;
    char str[50] ;
    int n ;
    fstream file ;

    file.open("PatientList.dat",ios::in|ios::out|ios::binary|ios::ate);

                if(!file)
                {
                    Screen();
                    sprintf( str , " No data Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
                }

                else
                {

                      n = file.tellp() / sizeof(p) ;

                      Screen();
                      BOX(5,35,24,95,11,1);

                      sprintf(str," Total Records Found  %d",n);
                      textrc(str,6,37,14,3,0);

                      sprintf(str," Enter Patient Id  ");
                      textrc(str,8,37,14,3,0);
                      cin>>x ;
                      x-- ;

                      if(x >= 0 && x< n)
                      {

                         file.close();
                         Pf.ShowSpecific(x);
                         fflush(stdin);
                         _getch;

                         sprintf(str,"Patient%d.dat",x+1);
                         file.open(str,ios::in|ios::binary|ios::ate);

                         if(!file)
                         {
                              Screen();
                              sprintf(str," No data FOund ");
                              textrc(str,6,37,14,3,0);
                              fflush(stdin);
                              _getch;
                         }

                         else
                         {
                             n = file.tellp() / sizeof(pdetail) ;

                             do
                             {

                                 file.seekp( (x)*sizeof(pdetail) , ios::beg );
                                 file.read( (char*)&pdetail ,sizeof(pdetail)  );
                                 pdetail.showpd() ;

                                 sprintf(str,"%4d OF %4d ",x+1,n);
                                 textrc(str,23,90,14,4,0);
                                 fflush(stdin) ;
                                 ch = _getch() ;

                                  if(ch==0 || ch== -32)
                                  {
                                        ch= _getch() ;

                                            if(ch == 80 || ch==77)
                                            {
                                                x++ ;
                                                if(x == n)
                                                x = n-1 ;

                                            }

                                            else if(ch==72 || ch==75)
                                            {
                                                x-- ;
                                                if(x == -1)
                                                x = 0 ;
                                            }

                                    }

                             }while(ch != 27);


                         }


                       file.close();

                      }
                      else
                     {
                      file.close();
                      sprintf(str," Enter Valid Patient Id ");
                      textrc(str,10,37,14,3,0);
                      fflush(stdin);
                      _getch;
                     }

                }


}

void PatientDetail::ProvideToPatient()
{
    PatientDetail pdetail ;
    char ch,str[50] ;
    Patient p;
    BGroup b ;
    int totPat ,pd  ; /// Patient id pd ,


    fstream file,fbg,fp,fd ;

          file.open("PatientList.dat",ios::in|ios::ate|ios::binary);

            if(!file)
            {
                    Screen();
                    sprintf( str , " No Patient Found "  );
                    textrc(str,6,37,14,3,0);
                    fflush(stdin);
                    _getch;
                    return ;

            }

            else
            {
                totPat = file.tellg() / sizeof(p) ;

            }

            file.close();

            fp.open("PatientList.dat",ios::in|ios::out|ios::binary);

            do
            {
                      Screen();
                      BOX(5,35,24,95,11,1);


                      sprintf(str," Enter Patient Id ");
                      textrc(str,6,37,14,3,0);

                      cin>>pd ;
                      pd-- ;


                      if(pd < 0 || pd >= totPat)
                      {
                          sprintf(str," Enter Valid Patient Id ");
                          textrc(str,8,37,14,3,0);

                          sprintf(str," Give to other Patient (^Y/^N) ");
                          textrc(str,10,37,14,3,0);
                          fflush(stdin);
                          ch = getche() ;
                          continue ;
                      }


                      fp.seekp( pd*sizeof(p) , ios::beg );
                      fp.read( (char *)&p , sizeof(p) );
                      p.ShowPatient();
                      fflush(stdin);
                      _getch;



                      BOX(5,35,25,105,11,1);

                      sprintf(str,"Enter Date of Providing ");
                      textrc(str,7,37,14,3,0);
                      pdetail.Tdate.GetDate(7,41);

                      sprintf(str,"   Quantity Provided    :");
                      textrc(str,12,37,14,3,0);
                      cin>>pdetail.Qty;


                      file.open("BloodGroup.dat",ios::in|ios::binary);
                      file.seekg( (p.Bgid-1)*sizeof(b),ios::beg);
                      file.read( (char *)&b , sizeof(b) );
                      file.close();

                      if(b.qty < pdetail.Qty)
                      {
                        sprintf(str," You Cannnot Recieve Blood !!! Only %d Left ",b.qty);
                        textrc(str,12,37,14,3,0);

                        sprintf(str," Provide To Other (^Y/^N) ");
                        textrc(str,14,37,14,3,0);
                        fflush(stdin);
                        ch = getche() ;
                        continue ;

                      }


                      sprintf(str," Provide Blood (^Y/^N) ");
                      textrc(str,14,37,14,3,0);
                      fflush(stdin);
                      ch = getche();

                      if( ch=='Y' || ch== 'y')
                      {

                         b.qty -= pdetail.Qty  ;


                        file.open("BloodGroup.dat",ios::in|ios::out|ios::binary);
                        file.seekp( (p.Bgid-1)*sizeof(b),ios::beg);
                        file.write( (char *)&b , sizeof(b) );
                        file.close();



                        sprintf(str,"Patient%d.dat",p.Pid);
                        file.open(str,ios::in|ios::out|ios::binary|ios::ate);

                        if(!file)
                            file.open(str,ios::out|ios::binary);


                        file.write( (char*)&pdetail , sizeof(pdetail));
                        file.close();

                        p.ltdate = pdetail.Tdate ;
                        p.Qty += pdetail.Qty     ;


                        fp.seekp( pd*sizeof(p) , ios::beg );
                        fp.write( (char *)&p , sizeof(p) );


                        sprintf(str," Data Saved !!! ");
                        textrc(str,16,37,14,3,0);





                      }

                      sprintf(str," Provide To Other Patient (^Y/^N) ");
                      textrc(str,18,37,14,3,0);
                      fflush(stdin);
                      ch = getche();




            }while(ch=='Y' || ch=='y');

            fp.close();



}

void EntriesMenu()
{
       char mn[3][40]=
       {
            "^New ^Donor",
            "^New ^Patient",
            "^Back to ^Main^Menu",

       };

       int op=0;
       PatientFile pf ;
       DonorFile df;
       do
       {
            Screen();
            op=showMenu(mn,3,58,170,op,14,5,2);


            switch (op)
            {
               case 0:
                   df.EnterDonor();
                   break;

               case 1:
                   pf.EnterPatient();
                   break;

            }

       }while(op!=2);

}

void EditMenu()
{
     char mn[3][40]=
       {
            "^Edit ^Donor ",
            "^Edit ^Patient",
            "^Back to ^Main^Menu",

       };
       int op=0;
       PatientFile pf ;
       DonorFile df;
       do
       {
            Screen();
            op=showMenu(mn,3,58,170,op,14,5,2);


            switch (op)
            {
               case 0:
                   df.EditDonor();
                   break;

               case 1:
                   pf.EditPatient();
                   break;

            }

       }while(op!=2);

}

void TransactionMenu()
{
     char mn[3][40]=
       {
            "^Recieve ^Blood ",
            "^Provide ^To ^Patient",
            "^Back to ^Main^Menu",

       };
       int op=0;
       DonorDetail dd;
       PatientDetail pd ;
       do
       {
            Screen();
            op=showMenu(mn,3,58,170,op,14,5,2);


            switch (op)
            {
               case 0:
                   dd.RecieveBlood();
                   break;

               case 1:
                   pd.ProvideToPatient();
                   break;

            }

       }while(op!=2);

}


void ShowMenu()
{
    char mn[5][40]=
       {
            "^Show ^All ^Donors",
            "^Show ^Specific ^Donors",
            "^Show ^All ^Patients",
            "^Show ^Specific ^Patients",
            "^Back ^To ^Main^Menu"
       };
       int op=0;
       PatientFile pf ;
       DonorFile df;
       do
       {
            Screen();
            op=showMenu(mn,5,58,170,op,14,5,2);


            switch (op)
            {
               case 0:
                   df.ShowAll();
                   break;

               case 1:
                   df.ShowSpecific();
                   break;

               case 2:
                   pf.ShowAll();
                   break;

               case 3:
                   pf.ShowSpecific();
                   break;



            }

       }while(op!=4);

}

void ReportsMenu()
{
       char mn[4][40]=
       {
            "^Blood ^IN ^Stock",
            "^Donors",
            "^Patients",
            "^Back ^To ^Main^Menu"
       };

       int op=0;
       PatientDetail pd ;
       DonorDetail dd;
       BGroup b;
       do
       {
            Screen();
            op=showMenu(mn,4,58,170,op,14,5,2);


            switch (op)
            {
               case 0:
                   b.ShowAll();
                   break;

               case 1:
                   dd.ShowDetail();
                   break;

               case 2:
                   pd.ShowDetail();
                   break;

            }

       }while(op!=3);

}



void MainMenu()
{
     char mn[6][40] =
       {
            "^Entries",
            "e^Dit",
            "^Transaction",
            "^Report",
            "^Show",
            "e^Xit"
       };
       int op=0;
       do
       {
            Screen();
            op=showMenu(mn,6,58,170,op,14,5,2);


            switch (op)
            {
               case 0:
                   EntriesMenu();
                   break;

               case 1:
                   EditMenu();
                   break;

               case 2:
                   TransactionMenu();
                   break;

               case 3:
                   ReportsMenu();
                   break;

               case 4:
                   ShowMenu();
                   break;


            }

       }while(op!=5);



}


int main()
{

     char pwd[7];
     char str[100];
     int i=0;
     cout<<"\n Enter Password (Case Sensitive) : " ;
     while(i<7 )
    {
      pwd[i]=_getch();
      if(pwd[i] == 13)
           break;

      cout<<"*";
      ++i;
    }


    if ( strcmp(pwd,"anirudh") == 1 )
    {
        cout<<"\n Correct Password !! Press Any key " ;
        _getch;
        MainMenu();


        Screen();
        BOX(5,35,15,105,14,3);

        sprintf(str,"%-12s", " Thank you For Seeing The Project ");
        textrc(str,6,37,14,3,0);

        sprintf(str,"%-12s", " Special Thanks To : ");
        textrc(str,8,37,14,3,0);

        sprintf(str,"%-12s", " Mr. Abhijeet Dhole ");
        textrc(str,9,57,14,3,0);

        sprintf(str,"%-12s", " Mrs. Manju Sao ");
        textrc(str,10,57,14,3,0);

        sprintf(str,"%-12s", " Submitted By : Anirudh Maheshwari ");
        textrc(str,12,37,14,3,0);

        sprintf(str,"%-12s", " Roll no.     : ");
        textrc(str,13,37,14,3,0);

        _getch;

    }

    else
    {
        cout<<"\n"<<pwd<<" Is WRONG  password !!!! ";
        _getch;
    }

}



