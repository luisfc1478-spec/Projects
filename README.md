import time
import random
import emoji
import os

def limpar_tela():
    os.system('cls' if os.name == 'nt' else 'clear')

def pausar():
    time.sleep(1)

def linhas():
    print(30 * '-')

def atribuir_saldo():
    while True:
        try:
            saldo_inicial = float(input('Quanto dinheiro pretende trocar por fichas? '))
            if saldo_inicial <= 0:
                print('O valor deve ser maior que zero. Tente novamente.')
                pausar()
            else:
                return saldo_inicial
        except ValueError:
            print('Entrada inválida. Por favor, insira um número válido.')
            pausar()




limpar_tela()
emo = emoji.emojize(':slot_machine:')
nome = f'{emo} CASINO {emo}'

linhas()
print(f'{nome:^30}')
linhas()

pausar()

print('Bem-vindo ao Casino!')
pausar()
saldo = atribuir_saldo()

pausar()
while True:


    if saldo == 0:
        print('Foi expulso do Casino por falta de fichas! Volte sempre!')
        break
    print('Menu de jogos:')
    print('[1] Máquina de Slots\n[2] Roleta\n[3] Blackjack\n[4] Sair do Casino')
    escolha = input('Qual jogo deseja jogar? ').strip()
    linhas()

    #MÁQUINA DE SLOTS
    # Luis e Anxo
    if escolha == '1':
        
        limpar_tela()
        print('Bem-Vindo à Máquina de Slots!')
        pausar()

        while True:

            aposta = float(input('Quanto deseja apostar? '))

            if aposta > saldo:
                print('Saldo insuficiente para essa aposta. Tente novamente.')
                continue

            saldo -= aposta
            limpar_tela()
            lista = ['🍒', '🍋', '🍊', '💎', '⭐', '7️⃣']
            for i in range(15):
                print('Girando' + '.' * (i + 1))
                slot1 = random.choice(lista)
                slot2 = random.choice(lista)
                slot3 = random.choice(lista)

                print(f'| {slot1} | {slot2} | {slot3} |')
                time.sleep(0.1 + i * 0.05)
                if i < 14:
                    limpar_tela()

            if slot1 == slot2 == slot3:
                if slot1 == '7️⃣':
                    ganhos = aposta * 10
                elif slot1 == '💎':
                    ganhos = aposta * 5
                elif slot1 == '⭐':
                    ganhos = aposta * 3
                else:
                    ganhos = aposta * 2

                saldo += ganhos
                print(f'Parabéns! Ganhou {ganhos:.2f} fichas!')
            else:
                print('Não ganhou desta vez. Tente novamente!')

            print(f'Seu saldo atual é de {saldo:.2f} fichas.')
            linhas()

            continuar = input('Deseja jogar novamente na Máquina de Slots? [S/N] ').strip().upper()
            if continuar == 'N':
                limpar_tela()
                break
            else:
                limpar_tela()

    #ROLETA
    # Anxo
    elif escolha == '2':
        
        limpar_tela()
        print('Bem-Vindo à Roleta!')
        pausar()

        while True:

            if saldo == 0:
                print('Seu saldo está zerado. Não é possível continuar jogando.')
                break

            aposta = float(input('Quanto deseja apostar? '))

            if aposta > saldo:
                print('Saldo insuficiente para essa aposta. Tente novamente.')
                continue

            tipo_aposta = input('Deseja apostar em "Número" ou "Cor"? ').strip().capitalize()

            saldo -= aposta
            numero_sorteado = random.randint(0, 36)

            if numero_sorteado == 0:
                cor_sorteada = 'Verde'
            elif numero_sorteado % 2 == 0:
                cor_sorteada = 'Vermelho'
            else:
                cor_sorteada = 'Preto'

            if tipo_aposta in ['Número', 'Numero', 'N']:
                numero_escolhido = int(input('Escolha um número de 0 a 36: '))
                pausar()
                print('Sorteando o número...')
                time.sleep(3)

                if numero_escolhido == numero_sorteado:
                    ganhos = aposta * 50
                    saldo += ganhos
                    print(f'Parabéns! Ganhou {ganhos:.2f} fichas!')
                else:
                    print('Não ganhou desta vez...')

            elif tipo_aposta in ['Cor', 'C']:
                cor_escolhida = input('Escolha uma cor (Vermelho, Preto, Verde): ').strip().capitalize()
                pausar()
                print('Sorteando a cor...')
                time.sleep(3)
                if cor_escolhida == cor_sorteada:
                    ganhos = aposta * (35 if cor_escolhida == 'Verde' else 2)
                    saldo += ganhos
                    print(f'Parabéns! Ganhou {ganhos:.2f} fichas!')
                    pausar()
                else:
                    print('Não ganhou desta vez...')

            print(f'O número sorteado foi {numero_sorteado} - {cor_sorteada}.')
            pausar()
            print(f'Seu saldo atual é de {saldo:.2f} fichas.')
            linhas()

            continuar = input('Deseja jogar novamente na Roleta? [S/N] ').strip().upper()
            if continuar == 'N':
                limpar_tela()
                break
            else:
                limpar_tela()


    #BLACKJACK
    # Luis
    elif escolha == '3':
        
        limpar_tela()
        print('Bem-Vindo ao Blackjack!')
        pausar()

        while True:

            if saldo == 0:
                print('Seu saldo está zerado. Não é possível continuar jogando.')
                break

            aposta = float(input('Quanto deseja apostar? '))

            if aposta > saldo:
                print('Saldo insuficiente para essa aposta. Tente novamente.')
                continue

            saldo -= aposta

            cartas = [2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10, 11]

            jogador = [random.choice(cartas), random.choice(cartas)]
            dealer = [random.choice(cartas), random.choice(cartas)]

            jogador_total = sum(jogador)
            dealer_total = sum(dealer)

            pausar()
            print('Distribuindo as cartas...')
            time.sleep(3)
            print(f'Suas cartas: {jogador}, total: {jogador_total}')
            pausar()
            print(f'A primeira carta do dealer é {dealer[0]}.')
            pausar()

            # Jogador pede ou para
            while jogador_total < 21:
                acao = input('Deseja "Pedir" ou "Parar"? ').strip().capitalize()

                if acao == 'Pedir':
                    nova = random.choice(cartas)
                    jogador.append(nova)
                    jogador_total = sum(jogador)
                    pausar()
                    print(f'Suas cartas: {jogador}, total: {jogador_total}')
                    pausar()
                else:
                    break

            if jogador_total > 21:
                print('Estourou! Você perdeu.')
            else:

            # Dealer compra até 17
                while dealer_total < 17:
                    dealer.append(random.choice(cartas))
                    dealer_total = sum(dealer)

                print(f'Cartas do dealer: {dealer}, total: {dealer_total}')
                pausar()

                if dealer_total > 21 or jogador_total > dealer_total:
                    ganhos = aposta * 2
                    saldo += ganhos
                    print(f'Parabéns! Ganhou {ganhos:.2f} fichas!')
                elif jogador_total == dealer_total:
                    saldo += aposta
                    print('Empate! Sua aposta foi devolvida.')
                else:
                    print('O dealer venceu!')
            pausar()
            print(f'Seu saldo atual é de {saldo:.2f} fichas.')
            linhas()

            continuar = input('Deseja jogar novamente no Blackjack? [S/N] ').strip().upper()
            if continuar == 'N':
                limpar_tela()
                break 
            else:
                limpar_tela()
                
        

    #SAIR

    elif escolha == '4':
        
        limpar_tela()
        print('Obrigado por visitar o Casino! Volte sempre!')
        break

    else:
        print('Opção inválida. Tente novamente.')
