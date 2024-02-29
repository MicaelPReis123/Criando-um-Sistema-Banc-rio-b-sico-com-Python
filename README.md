# Criando-um-Sistema-Banc-rio-b-sico-com-Python
# Nesse Código eu faço um sistema de banco em Python em que temos funções de saque, deposito, verificação de saldo.  
global saldo
global deposito 
saldo = 0
deposito = 0

import random

#Gera um novo ID de conta 
def gerar_id_conta(): #gera um id aléatorio para contas dos clientes 
    agencia = '0022-2'
    numero_aleatorio = ''.join(str(random.randint(0, 9)) for _ in range(6))
    id_conta = f'{agencia}  {numero_aleatorio}'
    return id_conta

bdusuario = {}

def cliente():
    usuario_cadastrado = input('Digite seu CPF: ')
 #Impede que o usuario que já é cadastrado faça outra conta 
    if usuario_cadastrado in bdusuario:
        print("Você já tem conta no nosso banco, acesse as outras opções!")
        menu(usuario_cadastrado) 

    else:
        novo_usuario = {
            'nome': input('Digite seu nome: '),
            'telefone': input('Digite seu telefone: '),
            'email': input('Digite seu e-mail: '),
            'endereco': input('Digite seu endereço: '),
            'tipo de conta': input('Qual o tipo de conta que deseja ter\nDigite 0 para ter conta Poupança\nDigite 1 para conta Corrente\n'),
            'saldo': 0,  # Inicializa o saldo do novo usuário como zero
            'Cartão de credito'
            'CPF': usuario_cadastrado
        }
        
        # Verifica se o ID da conta gerado já está em uso
        #O while any está verificando se o argumento é verdadeiro 
        #O .values faz a leitura de dos dados do bdusuario permite que o o id_conta faça o for e permite que o usuario leia o bdusuario
        id_conta = gerar_id_conta()
        while any(usuario['ID_conta'] == id_conta for usuario in bdusuario.values()):
            id_conta = gerar_id_conta()
        
        novo_usuario['ID_conta'] = id_conta
        bdusuario[usuario_cadastrado] = novo_usuario #nessa parte o novo_usuario se integra ao bdusuario, alem de integrar o id_conta
        menu(usuario_cadastrado)

        #conta Corrente para usuarios 
def conta_corrente():
    credito  = 300
    incremento_ponto = ()


def saque(usuario_cadastrado):
    limite_para_saque_diario = 3
    if limite_para_saque_diario != 0:
        saque = int(input('Digite o valor do saque:'))
        if bdusuario[usuario_cadastrado]['saldo'] >= saque:  # Verifica o saldo do usuário
            bdusuario[usuario_cadastrado]['saldo'] -= saque  # Atualiza o saldo do usuário
            limite_para_saque_diario -= 1
            print("Saque realizado com sucesso!")
        else:
            print(f"O valor que deseja sacar é maior do que seu saldo:\nSeu saldo é {bdusuario[usuario_cadastrado]['saldo']}")
    else:
        print("Seu limite de saque diário chegou ao fim por hoje, espere 24 horas para poder sacar novamente")

def saldo(usuario_cadastrado): 
    print(f"Seu saldo é de: {bdusuario[usuario_cadastrado]['saldo']}")

def deposito(usuario_cadastrado):
    deposito = int(input('Quanto deseja depositar? '))
    bdusuario[usuario_cadastrado]['saldo'] += deposito  # Atualiza o saldo do usuário
    print(f'Depósito realizado com sucesso! Seu saldo atual é {bdusuario[usuario_cadastrado]["saldo"]}')

def menu(usuario_cadastrado): 
    while True: 
        escolha = input('''
    ================================================= Menu =================================================
    + Digite [Sacar] para realizar o saque ou  [1]                                                          +
    + Digite [Deposito] para depositar ou      [2]                                                              +
    + Digite [Saldo] para verificar o saldo ou [3]                                                         +
    + Digite [Sair] para encerrar o sistema ou [4]                                                         +
    ================================================= Menu ================================================= 
        ''')
        #A função que sera chamado de acordo com com a escolha do usuario
        if escolha.lower() == 'sacar' or escolha == '1':
            saque(usuario_cadastrado)
        elif escolha.lower() == 'deposito' or escolha == '2':
            deposito(usuario_cadastrado)
        elif escolha.lower() == 'saldo' or escolha == '3':
            saldo(usuario_cadastrado)
        elif escolha.lower() == 'sair' or escolha == '4':
            print('Encerramento concluído. Obrigado pela preferência.')
            break
        else:
            print('Opção inválida!')


cliente()  # Inicia o sistema pedindo o CPF do usuário
