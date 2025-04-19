arquivo_estoque = "estoque.txt"

lista = []
try:
    arquivo = open(arquivo_estoque, "r")
    for linha in arquivo:
        codigo, nome, qtd, unidade, preco, validade = linha.strip().split(";")
        lista.append([codigo, nome, qtd, unidade, preco, validade])
    arquivo.close()
except FileNotFoundError:
    pass  # Arquivo ainda não existe


while True:
    print("\n=== MENU ESTOQUE ===")
    print("1. Cadastrar produto")
    print("2. Ver todos os produtos")
    print("3. Sair")
    opcao = input("Escolha uma opção: ")

    if opcao == "1":
        codigo = input("Código do produto: ")
        nome = input("Nome: ")
        qtd = input("Quantidade: ")
        unidade = input("Unidade (ex: kg, un): ")
        preco = input("Preço unitário: ")
        validade = input("Data de validade (AAAA-MM-DD): ")

        lista.append([codigo, nome, qtd, unidade, preco, validade])

       
        arquivo = open(arquivo_estoque, "w")
        for item in lista:
            linha = ";".join(item) + "\n"
            arquivo.write(linha)
        arquivo.close()
        print("Produto cadastrado com sucesso!")

    elif opcao == "2":
        if len(lista) == 0:
            print("Estoque vazio.")
        else:
            print("\n--- ESTOQUE ---")
            for item in lista:
                print(f"Código: {item[0]}, Nome: {item[1]}, Quantidade: {item[2]} {item[3]}, Preço: R${item[4]}, Validade: {item[5]}")
    
    elif opcao == "3":
        print("Saindo...")
        break

    else:
        print("Opção inválida. Tente de novo.")

