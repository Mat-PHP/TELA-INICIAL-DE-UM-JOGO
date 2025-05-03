import pygame
import sys
import random

pygame.init()

# Tela
largura, altura = 800, 600
tela = pygame.display.set_mode((largura, altura))
pygame.display.set_caption("Jogo do Brasil")

# Cores
VERDE = (0, 153, 0)
AMARELO = (255, 204, 0)
AZUL = (0, 102, 204)
BRANCO = (255, 255, 255)
PRETO = (0, 0, 0)

# Fonte
fonte = pygame.font.SysFont("comicsansms", 36)

# Estados
TELA_MENU = "menu"
TELA_OPCOES = "opcoes"
TELA_JOGO = "jogo"
estado_atual = TELA_MENU

# Controles padrão
controles = {"mover_esquerda": pygame.K_LEFT, "mover_direita": pygame.K_RIGHT}

# Personagens (simples blocos coloridos por enquanto)
personagens = [(255, 0, 0), (0, 255, 0), (0, 0, 255)]
personagem_atual = None
personagem_pos = [400, 300]

# Função: desenhar botão
def desenhar_botao(texto, x, y, largura, altura, cor, cor_texto):
    pygame.draw.rect(tela, cor, (x, y, largura, altura))
    render = fonte.render(texto, True, cor_texto)
    tela.blit(render, (x + 20, y + 10))
    return pygame.Rect(x, y, largura, altura)

# Função: gerar personagem aleatório
def gerar_personagem():
    global personagem_atual
    personagem_atual = random.choice(personagens)

# Loop principal
rodando = True
while rodando:
    tela.fill(VERDE)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            rodando = False

        if event.type == pygame.MOUSEBUTTONDOWN and event.button == 1:
            mouse_pos = pygame.mouse.get_pos()

            if estado_atual == TELA_MENU:
                if btn_iniciar.collidepoint(mouse_pos):
                    gerar_personagem()
                    estado_atual = TELA_JOGO
                elif btn_opcoes.collidepoint(mouse_pos):
                    estado_atual = TELA_OPCOES
                elif btn_sair.collidepoint(mouse_pos):
                    rodando = False

            elif estado_atual == TELA_OPCOES:
                if btn_voltar.collidepoint(mouse_pos):
                    estado_atual = TELA_MENU

            elif estado_atual == TELA_JOGO:
                pass  # Aqui vai a lógica do jogo em si

    # Telas
    if estado_atual == TELA_MENU:
        titulo = fonte.render("Jogo do Brasil!", True, AMARELO)
        tela.blit(titulo, (250, 50))
        btn_iniciar = desenhar_botao("Iniciar", 300, 200, 200, 60, AMARELO, AZUL)
        btn_opcoes = desenhar_botao("Opções", 300, 300, 200, 60, AMARELO, AZUL)
        btn_sair = desenhar_botao("Sair", 300, 400, 200, 60, AMARELO, AZUL)

    elif estado_atual == TELA_OPCOES:
        tela.fill(AZUL)
        tela.blit(fonte.render("Configurações", True, BRANCO), (280, 50))
        tela.blit(fonte.render("Controles: ← →", True, BRANCO), (200, 150))
        tela.blit(fonte.render("Gráficos: Médio", True, BRANCO), (200, 220))
        btn_voltar = desenhar_botao("Voltar", 300, 400, 200, 60, AMARELO, AZUL)

    elif estado_atual == TELA_JOGO:
        tela.fill(PRETO)
        if personagem_atual:
            pygame.draw.rect(tela, personagem_atual, (*personagem_pos, 50, 50))
        tela.blit(fonte.render("Pressione ESC para voltar", True, BRANCO), (220, 550))

        keys = pygame.key.get_pressed()
        if keys[controles["mover_esquerda"]]:
            personagem_pos[0] -= 5
        if keys[controles["mover_direita"]]:
            personagem_pos[0] += 5
        if keys[pygame.K_ESCAPE]:
            estado_atual = TELA_MENU

    pygame.display.update()

pygame.quit()
sys.exit()
