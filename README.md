#include<stdio.h>

//PLACEMENT MANAGEMENT STSTEM
#include<conio.h>

#include<string.h>

#include<process.h>

#include<stdlib.h>

#include<dos.h>

#include<float.h>

struct placement

{

    long long ph, roll_no;

    char name[20],add[40],email[30],branch[20],pakage[20];

    float percent;

};

char pakage[20];

void pakage_check(float);



int main()

{
	struct placement list;
long long query,roll_no;

FILE *fp, *fd;

char branch[10][10]={"CSE","IT","ECE","ME"};

int i,n,ch,len,found,del,k;



main:

    system("cls");    //-----------Main menu----------------//

    printf("\n\t !!!!!!!!!!! Welcome to Placement Management System !!!!!!!!!!!");

    printf("\n\n\n\t\t\t***** MAIN MENU *****\n\t\t____________________________________\n\t\t(1) Add a New Student\n\t\t(2) List of Student's Record\n\t\t(3) Search for a Student's Record\n\t\t(4) Edit a Student's Record\n\t\t(5) Delete a Student's Record\n\t\t(0) Exit\n\t\t____________________________________\n\t\t");

    printf("Enter the choice:");

    scanf("%d",&ch);

    switch(ch)

    {

    case 0:

        printf("\n\n\t\tAre you sure you want to exit?");

        break;

        //-----------------Add new student-----------------//

    case 1:

        system("cls");

        fp=fopen("student_details.txt","a");

        fflush(stdin);

        printf("\n\t\t\n\t\t\t***** ADD A NEW STUDENTS *****\n\t\t\n *=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=**=*=*=*=*=*=*=*=*=*\n\n");

        while(1)

        {
            fflush(stdin);

            printf(" ______________________________________________________________________________\n");

            printf(" To exit enter space bar/ input the name :");

            printf("\n Name     :");

             scanf("%[^\n]",&list.name);

            if(stricmp(list.name,"")==0 || stricmp(list.name," ")==0)

                break;

     	fflush(stdin);

        printf(" Roll_no  :");

        scanf("%llu",&list.roll_no);

        fflush(stdin);

        printf(" Branch   :");

        scanf("%[^\n]",&list.branch);

        fflush(stdin);

        printf(" Percent  :");

        scanf("%f",&list.percent);

        fflush(stdin);

        pakage_check(list.percent);

        strcpy(list.pakage,pakage);

        printf(" Phone    :");

        scanf("%llu",&list.ph);

        fflush(stdin);

        printf(" Address  :");

        scanf("%[^\n]",&list.add);

        fflush(stdin);

        printf(" Email    :");

        gets(list.email);

        printf("\n");

        printf(" ______________________________________________________________________________\n");

        getch();

        fwrite(&list,sizeof(list),1,fp);

        }

        fclose(fp);

        break;

						//---------------list of student---------------//

    case 2:


        system("cls");

        printf("\n\t\t\n\t\t\t***** LIST OF STUDENTS *****\n\t\t\n *=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=**=*=*=*=*=*=*=*=*=*\n\n");

		for(i=0;i<=3;i++)

        {
        	strupr(branch[i]);

        	printf("\n Branch :%s",branch[i]);

        	printf(" \n ______________________________________________________________________________");

            fp=fopen("student_details.txt","r");

            fflush(stdin);

            found=0;

            while(fread(&list,sizeof(list),1,fp)==1)

            {
            	strupr(list.branch);

                if(stricmp(list.branch,branch[i])==0)

                {

                    printf("\n Name     : %s\n Roll NO  : %llu\n Branch   : %s\n Percent  : %f%%\n Elligible: %s\n Pacakage\n Phone    : %llu\n Address  : %s\n Email    : %s\n",list.name,list.roll_no,list.branch,list.percent,list.pakage,

                           list.ph,list.add,list.email);
                    printf(" ______________________________________________________________________________");


                    found++;

                }

            }

            if(1)

            {
                printf("\n No. of students in branch %s: %d\n\n",branch[i],found);

                printf("\n *=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=**=*=*=*=*=*=*=*=*=*\n\n");

                getch();
            }

            fclose(fp);

        }

        break;

        //---------------search students---------------//

    case 3:

        system("cls");

        do

        {

            found=0;

            printf("\n\t\t\n\t\t\t***** SEARCH STUDENT'S DETAILS *****\n\t\t\n *=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=**=*=*=*=*=*=*=*=*=*\n\n Roll no. of student to search: ");

            fflush(stdin);

            scanf("%llu",&query);

            fp=fopen("student_details.txt","r");

            system("cls");

            printf("\n\t\t\n\t\t\t***** SEARCH STUDENT'S STUDENTS *****\n\t\t\n *=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=**=*=*=*=*=*=*=*=*=*\n\n");

            printf(" Search result for roll no. : %llu \n ______________________________________________________________________________",query);

            while(fread(&list,sizeof(list),1,fp)==1)

            {

                    roll_no=list.roll_no;


                if(roll_no==query)

                {

                    printf("\n Name     : %s\n Roll NO  : %llu\n Branch   : %s\n Percent  : %f%%\n Elligible: %s\n Pacakage\n Phone    : %llu\n Address  : %s\n Email    : %s\n",list.name,list.roll_no,list.branch,list.percent,list.pakage,

                           list.ph,list.add,list.email);

                    found++;

                }

            }

            if(found==0)

                printf("\n\t\t\tNo match found!");


            fclose(fp);

            printf("\n ______________________________________________________________________________\n");

            printf("\n Try again?\n\n\t[1] Yes\t\t[0] No\n\t");

            scanf("%d",&ch);

        }
        while(ch==1);

        break;

        //9---------edit student's details---------------//

    case 4:

    	try_again:

        fp=fopen("student_details.txt","r");

        fd=fopen("temp.txt","w");

        system("cls");

        fflush(stdin);

        printf("\n\t\t\n\t\t\t***** EDIT STUDENT'S DETAILS *****\n\t\t\n *=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=**=*=*=*=*=*=*=*=*=*\n\n");

        printf(" Enter the roll no. :");

        scanf("%llu",&query);

        found=0;

        while(fread(&list,sizeof(list),1,fp)==1)

        {
        	roll_no=list.roll_no;

            if(roll_no!=query)

                fwrite(&list,sizeof(list),1,fd);


            else if(roll_no==list.roll_no)
            {
			printf("\n EXISTING DETAILS:\n ______________________________________________________________________________");

            printf("\n Name     : %s\n Roll NO  : %llu\n Branch   : %s\n Percent  : %f%%\n Elligible: %s\n Pacakage\n Phone    : %llu\n Address  : %s\n Email    : %s\n",list.name,list.roll_no,list.branch,list.percent,list.pakage,

                           list.ph,list.add,list.email);
            printf(" ______________________________________________________________________________");

        	getch();

        	found++;

			}


        }


        if(found==0)
        {
        	invalid_choice:

        	printf("\n No Student Found\n\n Try Again :\n (1)Yes\t\t(0)No\n");

        	scanf("%d",&k);

        	switch(k)
        	{
        		case 0:
        		goto student_not_found;

        		case 1:
        		goto try_again;

        		default:
        			{

						printf("\n\n Invalid choice\n\n");
						goto invalid_choice;
					}

			}

		}


        system("cls");

        fflush(stdin);

        printf("\n\t\t\n\t\t\t***** EDIT STUDENT'S DETAILS *****\n\t\t\n *=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=**=*=*=*=*=*=*=*=*=*\n\n");

        printf(" Editing details of roll no: %llu\n\n",query);

         printf("\n Enter the new details of the student:\n");

        printf(" ______________________________________________________________________________\n");

        printf(" Name     :");

        scanf("%[^\n]",&list.name);

        fflush(stdin);

        printf(" Roll_no  :");

        scanf("%llu",&list.roll_no);

        fflush(stdin);

        printf(" Branch   :");

        scanf("%[^\n]",&list.branch);

		fflush(stdin);

        printf(" Percent  :");

        scanf("%f",&list.percent);

        fflush(stdin);

        pakage_check(list.percent);

        strcpy(list.pakage,pakage);

        printf(" Phone    :");

        scanf("%llu",&list.ph);

        fflush(stdin);

        printf(" Address  :");

        scanf("%[^\n]",&list.add);

        fflush(stdin);

        printf(" Email    :");

        gets(list.email);

        printf("\n");

        printf(" ______________________________________________________________________________\n");

        getch();

        fwrite(&list,sizeof(list),1,fd);

        system("cls");



        printf("\n\t\t\n\t\t\t***** EDIT STUDENT'S DETAILS *****\n\t\t\n *=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=**=*=*=*=*=*=*=*=*=*\n\n");

        printf("\n EDITED DETAILS:\n ______________________________________________________________________________");

        printf("\n Name     : %s\n Roll NO  : %llu\n Branch   : %s\n Percent  : %f%%\n Elligible: %s\n Pacakage\n Phone    : %llu\n Address  : %s\n Email    : %s\n",list.name,list.roll_no,list.branch,list.percent,list.pakage,

                           list.ph,list.add,list.email);
        printf(" ______________________________________________________________________________");

        getch();

        student_not_found:

        fclose(fp);

        fclose(fd);

        remove("student_details.txt");

        rename("temp.txt","student_details.txt");



        break;

        //---------------delete student's details---------------//

    case 5:

        system("cls");

        fflush(stdin);

        printf("\n\t\t\n\t\t\t***** DELETE STUDENT'S DETAILS *****\n\t\t\n *=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=**=*=*=*=*=*=*=*=*=*\n\n");

        printf(" Enter the the roll no.: ");

		scanf("%llu",&query);

        fp=fopen("student_details.txt","r");

        fd=fopen("temp.txt","w");

        while(fread(&list,sizeof(list),1,fp)!=0)

			{
				if (query==list.roll_no)

				{

				printf("\n EXISTING DETAILS:\n ______________________________________________________________________________");

            	printf("\n Name     : %s\n Roll NO  : %llu\n Branch   : %s\n Percent  : %f%%\n Elligible: %s\n Pacakage\n Phone    : %llu\n Address  : %s\n Email    : %s\n",list.name,list.roll_no,list.branch,list.percent,list.pakage,

                           list.ph,list.add,list.email);
            	printf(" ______________________________________________________________________________");


        		printf("\n ARE YOU SURE!\n Press :\n (1)Yes\t\t(0)No\n ");

        		scanf("%d",&del);

        		switch (del)

       			{

    				case 0:

        				goto exit;

    				case 1:

        				break;

    				default:

        				printf("Invalid choice");

        			break;

    			}



				}

				if (query!=list.roll_no)

                fwrite(&list,sizeof(list),1,fd);
            }

        fclose(fp);

        fclose(fd);

        remove("student_details.txt");

        rename("temp.txt","student_details.txt");

        break;

    default:

        printf("Invalid choice");

        break;

    }

    exit:

    printf("\n\n\n Enter the Choice:\n (1)Main Menu\t\t(0)Exit\n ");

    scanf("%d",&ch);

    switch (ch)

    {

    case 1:

        goto main;

    case 0:

        break;

    default:

        printf("Invalid choice");

        break;

    }

	return 0;

}


void pakage_check(float percent)
{

		float p60=60,p70=70,p80=80;

		if(percent<p60)

        strcpy(pakage,"less than 3 LPA");

        if(percent>=p60&&percent<p70)

		strcpy(pakage,"Up to 5 LPA");

		if(percent>=p70&&percent<p80)

		strcpy(pakage,"Up to 9 LPA");

		if(percent>=p80)

		strcpy(pakage,"More than 9 LPA");


}
