# TTT
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
#include <stdbool.h>
#include <time.h>
#define side 3
#define COMPUTER 1 
#define HUMAN 2

bool RowCrossed(char board[side][side])
{
    for(int i=0;i<side;i++)
    {
        if(board[i][0]==board[i][1] && board[i][1]==board[i][2] && board[i][0]!=' ')
        return true;
    }
    return false;
}
bool ColumnCrossed(char board[side][side])
{
    for(int i=0;i<side;i++)
    {
        if(board[0][i]==board[1][i] && board[1][i]==board[2][i] && board[0][i]!=' ')
        return true;
    }
    return false;
}
bool DiagonalCrossed(char board[side][side])
{
    if(board[0][0]==board[1][1] && board[1][1]==board[2][2] && board[1][1]!=' ')
    return true;
    if(board[0][2]==board[1][1] && board[1][1]==board[2][0] && board[0][2]!=' ')
    return true;
    
    return false;
}

bool gameover(char board[side][side])
{
    return(RowCrossed(board)||ColumnCrossed(board)||DiagonalCrossed(board));
}

void declareWinner(int turn)
{
    if(turn==HUMAN)
    printf("\t\t Congratulations You are the Winner of this game...!!!");
    else
    printf("\t\t OOPS! You have lost this game...!!!");
}

void showboard(char board[side][side])
{
    for(int i=0;i<side;i++)
    {
        printf("\t\t\t");
        for(int j=0;j<side;j++)
        {
            if(j!=2)
            printf(" %c |",board[i][j]);
            else
            printf(" %c ",board[i][j]);
        }
        printf("\n");
        printf("\t\t\t ----------\n");
    }
    printf("\n\n");
}

void HumanTurnFunc(char board[side][side],int* turn,int* countTurns)
{
    char key;
    printf("\t\t\t Its your turn\n\n");
    scanf("%c",&key);
    if(key='1'&& board[0][0]==' ')
    board[0][0]='0';
    else if(key='2'&& board[0][1]==' ')
    board[0][1]='0';
    else if(key='3'&& board[0][2]==' ')
    board[0][2]='0';
    else if(key='4'&& board[1][0]==' ')
    board[1][0]='0';
    else if(key='5'&& board[1][1]==' ')
    board[1][1]='0';
    else if(key='6'&& board[1][2]==' ')
    board[1][2]='0';
    else if(key='7'&& board[2][0]==' ')
    board[2][0]='0';
    else if(key='8'&& board[2][1]==' ')
    board[2][1]='0';
    else if(key='9'&& board[2][2]==' ')
    board[2][2]='0';
    else
    {
        printf("\t\t\t Invalid Move\n\n");
        *turn=HUMAN;
        return;
    }
    showboard(board);
    *turn=COMPUTER;
    (*countTurns)++;
    return;
}

void PlayTicTacToe(int turn)
{
    srand(time(NULL));
    char board[side][side];
    for(int i=0;i<side;i++)
    {
        for(int j=0;j<side;j++)
        {
            board[i][j]=' ';
        }
    }
    
    printf("\t\t\t Play Tic-Tac-Toe\n\n");
    printf("\t\t You are playing Tic-Tac-Toe with computer\n\n");
    printf("\t Choose a cell numbered from 1 to 9 given below and play the game\n\n");
    printf("\t\t\t 1 | 2 | 3 \n");
    printf("\t\t\t ----------\n");
    printf("\t\t\t 4 | 5 | 6 \n");
    printf("\t\t\t ----------\n");
    printf("\t\t\t 7 | 8 | 9 \n\n\n");
    
    int x,y,countTurns=0;
    while(gameover(board)==false && countTurns!=side*side)
    {
        if(turn==COMPUTER)
        {
            x=rand()%side;
            y=rand()%side;
            if(board[x][y]==' ')
            {
                board[x][y]='X';
                printf("\t\t\t It's Computer's Turn\n\n");
                showboard(board);
                turn=HUMAN;
                countTurns++;
            }
            else
            {
                turn=COMPUTER;
            }
        }
        else if(turn==HUMAN)
        {
            HumanTurnFunc(board,&turn,&countTurns);
        }
    }
    if(gameover(board)==false && countTurns==side*side)
    {
        printf("\t\t\t It's a draw\n\n");
    }
    else
    {
        if(turn==HUMAN)
        turn=COMPUTER;
        else
        turn=HUMAN;
        declareWinner(turn);
    }
}

int main()
{
    PlayTicTacToe(HUMAN);
    return 0;
}
