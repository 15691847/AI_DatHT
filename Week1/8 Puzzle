#include<bits/stdc++.h>

#define REP(i , l , r) for(int i = l ; i <= r ; i++)
#define REPD(i , l , r) for(int i = l ; i >= r ; i--)
#define REPS(i , l , r) for(int i = l ; i < r ; i++)

typedef long long int ll;

using namespace std;

enum facing {
	LEFT , RIGHT , UP , DOWN , STAY
};

int puzzle[3][3] , posX , posY , checker;
// khoi tao cac node nhu la cac trang thai cua puzzle
class node{
	public :
		int arr[3][3] , x , y;
		string way;
		facing canFace;
		
		node(int a[3][3] , string way , facing canFace , int x , int y){
			this->way = way;
			this->canFace = canFace;
			this->x = x;
			this->y = y;
			REP(i,0,2){
				REP(j,0,2){
					arr[i][j] = a[i][j];
				}
			}
		}
		
		bool canMoveLeft(){
			return canFace != LEFT && y > 0;
		}
		bool canMoveRight(){
			return canFace != RIGHT && y < 2;
		}
		bool canMoveUp(){
			return canFace != UP && x > 0;
		}
		bool canMoveDown(){
			return canFace != DOWN && x < 2;
		}
		
		void moveLeft(){
			swap(arr[x][y] , arr[x][y-1]);
			y--;
			canFace = RIGHT;
			way += "l";
		}
		void moveRight(){
			swap(arr[x][y] , arr[x][y+1]);
			y++;
			canFace = LEFT;
			way += "r";
		}
		void moveUp(){
			swap(arr[x][y] , arr[x-1][y]);
			x--;
			canFace = DOWN;
			way += "u";
		}
		void moveDown(){
			swap(arr[x][y] , arr[x+1][y]);
			x++;
			canFace = UP;
			way += "d";
		}
		
		bool checkFinish(){
			if(checker == 1){
				REP(i,0,2){
					if(arr[0][i] != i+1 || arr[2][i] != 7-i) return false;;
				}
				return arr[1][0] != 8 || arr[1][2] != 4 ? false : true;
			}else{
				REP(i,0,2){
					if(arr[0][i] != i || arr[1][i] != i+3 || arr[2][i] != i+6) return false;
				}
				return true;
			}
			
		}
};

void moveLeft(){
	swap(puzzle[posX][posY] , puzzle[posX][posY-1]);
	posY--;
}
void moveRight(){
	swap(puzzle[posX][posY] , puzzle[posX][posY+1]);
	posY++;
}
void moveUp(){
	swap(puzzle[posX][posY] , puzzle[posX-1][posY]);
	posX--;
}
void moveDown(){
	swap(puzzle[posX][posY] , puzzle[posX+1][posY]);
	posX++;
}
// ham nhap du lieu
void initPuzzle(){
	cout << "Nhap cac gia tri cho puzzle : ";
	cin >> puzzle[0][0] >> puzzle[0][1] >> puzzle[0][2];
	cin >> puzzle[1][0] >> puzzle[1][1] >> puzzle[1][2];
	cin >> puzzle[2][0] >> puzzle[2][1] >> puzzle[2][2];
	
	bool checked = true;
	int sum = 0;
	REP(i,0,2){
		REP(j,0,2){
			sum += puzzle[i][j];
			if(puzzle[i][j] > 8) {
				checked = false;
				break;
			}
		}
	}
	if(sum != 36 || checked == false){
		cout << "Nhap sai du lieu vui long nhap lai" << endl;
		return initPuzzle();
	}
	
	REP(i,0,2){
		REP(j,0,2){
			if(puzzle[i][j] == 0){
				posX = i;
				posY = j;
				return;
			}
		}
	}
}
// ham in trang thai
void prin(){
	REP(i,0,2){
		REP(j,0,2){
			cout << puzzle[i][j] << " ";
		}
		cout << endl;
	}
}
// ham kiem tra xem da la trang thai dich chua		
bool checkFinish(){
	int counter1 = 0, counter2 = 0;
	REP(i,0,2){
		if(puzzle[0][i] == i+1) counter1++;
	}
	
	REP(i,0,2){
		if(puzzle[2][i] == 7-i) counter1++;
	}
	if(puzzle[1][0] == 8){
		counter1++;
	} 
	if(puzzle[1][2] == 4) {
		counter1++;
	}
	if(counter1 == 8) return true;
		
	REP(i,0,2){
		if(puzzle[0][i] == i) counter2++;
		if(puzzle[1][i] == i+3) counter2++;
		if(puzzle[2][i] == i+6) counter2++;
	}
	if(counter2 == 8) return true;
	return false;
}
// ham xac dinh trang thai dich
int countStart(){
	int sum = 0;
	REP(q,0,8){
		int row = q/3;
		int col = q%3;
		int counter = puzzle[row][col];
		REP(i,0,2){
			REP(j,0,2){
				if( (row < i && puzzle[i][j] < counter && puzzle[i][j] != 0 )  ){
					sum++;
				}else if(row == i && col < j && puzzle[i][j] < counter && puzzle[i][j] != 0){
					sum++;
				}
			}
		}
	}
	return sum;
}

int main(){
	int step = 0 ;
	ll numOfNode = 0;
	bool check = checkFinish();
	
	initPuzzle();
	const clock_t begin_time = clock();
	string way = "";
	node nd(puzzle , "" , STAY , posX , posY);
	vector<node> vt; // hang` doi
	vt.push_back(nd);
	
	checker = countStart() %2;
	cout << "Trang thai ban dau : " << endl;
	prin();
	cout << endl;
	while(!check){
		vector<node> open;
		REPS(i,0,vt.size()){
			numOfNode++;
			if(vt.at(i).checkFinish()){
				way = vt.at(i).way;
				check = true;
				break;
			}else{
				if(vt.at(i).canMoveLeft()){
					node nd = vt.at(i);
					nd.moveLeft();
					open.push_back(nd);
				}
				if(vt.at(i).canMoveRight()){
					node nd = vt.at(i);
					nd.moveRight();
					open.push_back(nd);
				}
				if(vt.at(i).canMoveUp()){
					node nd = vt.at(i);
					nd.moveUp();
					open.push_back(nd);
				}
				if(vt.at(i).canMoveDown()){
					node nd = vt.at(i);
					nd.moveDown();
					open.push_back(nd);
				}
			}
			
		}
		vt.clear();
		REPS(i,0,open.size()){
			vt.push_back(open.at(i));
		}
	}
	
	REPS(i,0,way.length()){
		if(way[i] == 'l'){
			moveLeft();
			prin();
			cout << "di chuyen sang trai" << endl << endl;
		}else if(way[i] == 'r'){
			moveRight();
			prin();
			cout << "di chuyen sang phai" << endl << endl;
		}else if(way[i] == 'u'){
			moveUp();
			prin();
			cout << "di chuyen len tren" << endl << endl;
		}else if(way[i] == 'd'){
			moveDown();
			prin();
			cout << "di chuyen xuong duoi" << endl << endl;
		}
	}
	cout << "Thuat toan BFS : " << endl;
	cout << "So buoc di = " << way.length() << endl;
	cout << "So phep toan da thuc hien = " << numOfNode << endl;
	cout << "Thoi gian tinh toan = " << float( clock () - begin_time ) /  CLOCKS_PER_SEC << "s";
	return 0;
}
