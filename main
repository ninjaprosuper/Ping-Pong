#include <iostream>
#include <array>
#include <thread>
#include <conio.h>
#include <list>

struct coordenadas
{
	int x;
	int y;

	bool operator==(const coordenadas& other)
	{
		return other.x == x && other.y == y;
	}
};

class jogadores
{
private:
	coordenadas posicoes;
	std::array <char, 2> teclas = {};
	size_t tamanho = 3;
	char representacao;
	int lado = 1;
public:
	jogadores(std::array <char, 2> input, coordenadas pos, char representacao)
	{
		for (size_t i = 0; i < teclas.size(); i++)
		{
			this->teclas[i] = input[i];
		}
		this->representacao = representacao;
		this->posicoes = pos;
	}

	coordenadas retornar_posicao()
	{
		return posicoes;
	}

	std::array <char, 2> retornar_teclas()
	{
		return teclas;
	}

	size_t retornar_tamanho()
	{
		return tamanho;
	}

	char retornar_representacao()
	{
		return representacao;
	}

	void mover(char &letra)
	{
		if (posicoes.y != 1)
		{
			if (letra == teclas[0])
			{
				posicoes.y -= 1;
				letra = 0;
			}
		}
		
		if (posicoes.y != 6)
		{
			if (letra == teclas[1])
			{
				posicoes.y += 1;
				letra = 0;
			}
		}
	}
};

class bola
{
private:
	
	coordenadas posicao;
	char representacao = 'O';
public:
	char lado = 'e';
	char direcao = 's';
	bola(coordenadas pos)
	{
		this->posicao.x = pos.x;
		this->posicao.y = pos.y;
	}

	coordenadas &retornar_coordenadas()
	{
		return posicao;
	}

	char retornar_representacao()
	{
		return representacao;
	}

	void movimentar()
	{
		if (lado == 'd')
		{
			posicao.x += 1;
		}
		else if (lado == 'e')
		{
			posicao.x -= 1;
		}

		if (direcao == 's')
		{
			posicao.y -= 1;
		}
		else if (direcao == 'd')
		{
			posicao.y += 1;
		}
	}

	char retornar_lado()
	{
		return lado;
	}

	char retornar_direcao()
	{
		return direcao;
	}

	void mudar_direcao()
	{
		if (direcao == 'd')
		{
			posicao.y -= 1;
			direcao = 's';
		}
		else if (direcao == 's')
		{
			posicao.y += 1;
			direcao = 'd';
		}
	}

	void mudar_lado()
	{
		if (lado == 'd')
		{
			posicao.x -= 1;
			lado = 'e';
		}
		else if (lado == 'e')
		{
			posicao.x += 1;
			lado = 'd';
		}
	}
};

class tabuleiro
{
private:
	std::array <std::array <char, 30>, 10> mapa;
public:
	void inicializar()
	{
		for (size_t i = 0; i < mapa.size(); i++)
		{
			for (size_t j = 0; j < mapa[i].size(); j++)
			{
				if (j == 0 || j == mapa[i].size() - 1 || i == 0 || i == mapa.size() - 1)
				{
					mapa[i][j] = 'X';
				}
				else
				{
					mapa[i][j] = ' ';
				}
			}
		}
	}

	void imprimir()
	{
		for (size_t i = 0; i < mapa.size(); i++)
		{
			for (size_t j = 0; j < mapa[i].size(); j++)
			{
				std::cout << mapa[i][j];
			}
			std::cout << "\n";
		}
	}

	void inserir_informacoes(jogadores player1, jogadores player2, bola bola_jogo)
	{
		coordenadas valores_mais;
		mapa[bola_jogo.retornar_coordenadas().y][bola_jogo.retornar_coordenadas().x] = bola_jogo.retornar_representacao();
		for (size_t i = 0; i < player1.retornar_tamanho(); i++)
		{
			mapa[player1.retornar_posicao().y + i][player1.retornar_posicao().x] = player1.retornar_representacao();
			mapa[player2.retornar_posicao().y + i][player2.retornar_posicao().x] = player2.retornar_representacao();
		}
	}

	bool encostou_parede(bola &bola_jogo)
	{
		if (bola_jogo.retornar_coordenadas().y == 0 || bola_jogo.retornar_coordenadas().y == mapa.size() - 1)
		{
			bola_jogo.mudar_direcao();
			return true;
		}
		return false;
	}

	bool rebater(bola &bola_jogo)
	{
		if (mapa[bola_jogo.retornar_coordenadas().y][bola_jogo.retornar_coordenadas().x] == '#' || mapa[bola_jogo.retornar_coordenadas().y][bola_jogo.retornar_coordenadas().x] == 'U')
		{
			bola_jogo.mudar_lado();
			return true;
		}
		return false;
	}

	bool ganhou(bool &ganhou, bola bola_jogo)
	{
		if (bola_jogo.retornar_coordenadas().x == 0)
		{
			ganhou = true;
			system("cls");
			std::cout << "\nPlayer1 ganhou!\n";
			return true;
		}
		else if (bola_jogo.retornar_coordenadas().x == 29)
		{
			ganhou = true;
			system("cls");
			std::cout << "\nPlayer2 ganhou!\n";
			return true;
		}

		return false;
	}
};

int main()
{
	using namespace std::chrono_literals;

	std::array <char, 2> input_1 = {'w','s'};
	std::array <char, 2> input_2 = { 'u','j'};
	coordenadas pos_1;
	coordenadas pos_2;
	pos_1.x = 28;
	pos_1.y = 4;
	pos_2.x = 1;
	pos_2.y = 4;
	tabuleiro mapa;
	jogadores player1(input_1, pos_1, '#');
	jogadores player2(input_2, pos_2, 'U');
	coordenadas pos_bola;
	pos_bola.x = 14;
	pos_bola.y = 5;
	bola bola_jogo({pos_bola});
	bool ganhou = false;
	char letra = 0;

	while (ganhou == false)
	{
		std::this_thread::sleep_for(200ms);
		system("cls");
		mapa.inicializar();
		mapa.inserir_informacoes(player1, player2, bola_jogo);
		if (_kbhit())
		{
			letra = _getch();
		}
		player1.mover(letra);
		player2.mover(letra);
		bola_jogo.movimentar();
		if (mapa.ganhou(ganhou, bola_jogo))
		{
			mapa.ganhou(ganhou, bola_jogo);
			return 0;
		}
		mapa.encostou_parede(bola_jogo);
		mapa.rebater(bola_jogo);
		mapa.imprimir();
	}
	return 0;
}
