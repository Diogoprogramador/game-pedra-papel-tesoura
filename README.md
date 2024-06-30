# game-pedra-papel-tesoura
import tkinter as tk
import random

# Funções para o jogo
def play(choice):
    global user_score, computer_score
    computer_choice = random.choice(['Pedra', 'Papel', 'Tesoura'])
    result = determine_winner(choice, computer_choice)
    update_result(result, choice, computer_choice)

def determine_winner(user, computer):
    if user == computer:
        return "Empate"
    elif (user == 'Pedra' and computer == 'Tesoura') or \
         (user == 'Papel' and computer == 'Pedra') or \
         (user == 'Tesoura' and computer == 'Papel'):
        global user_score
        user_score += 1
        return "Você ganhou!"
    else:
        global computer_score
        computer_score += 1
        return "Você perdeu!"

def update_result(result, user_choice, computer_choice):
    result_label.config(text=f"Você escolheu {user_choice}\nComputador escolheu {computer_choice}\n{result}")
    score_label.config(text=f"Pontos: Você {user_score} - {computer_score} Computador")

# Configuração da interface gráfica
root = tk.Tk()
root.title("Pedra, Papel e Tesoura")

user_score = 0
computer_score = 0

# Labels
result_label = tk.Label(root, text="Faça sua escolha!", font=('Arial', 14))
result_label.pack(pady=10)

score_label = tk.Label(root, text="Pontos: Você 0 - 0 Computador", font=('Arial', 12))
score_label.pack(pady=5)

# Botões com emoticons
buttons_frame = tk.Frame(root)
buttons_frame.pack(pady=20)

rock_button = tk.Button(buttons_frame, text="🪨 Pedra", font=('Arial', 12), command=lambda: play('Pedra'))
rock_button.grid(row=0, column=0, padx=10)

paper_button = tk.Button(buttons_frame, text="📄 Papel", font=('Arial', 12), command=lambda: play('Papel'))
paper_button.grid(row=0, column=1, padx=10)

scissors_button = tk.Button(buttons_frame, text="✂️ Tesoura", font=('Arial', 12), command=lambda: play('Tesoura'))
scissors_button.grid(row=0, column=2, padx=10)

# Loop principal
root.mainloop()
