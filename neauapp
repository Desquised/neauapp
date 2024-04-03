#!/usr/bin/env python3

import argparse
import urllib.parse
import requests
import os
import webbrowser
import readline
import time
import random
import sys
import uuid
from googletrans import Translator
from datetime import datetime

available_commands = ['neauapp', 'sv.o', 'path', 'echo $PATH', 'commands', 'help', 'clear', 'cls', 'date', 'translate', 'exit', 'ping', 'connected_users', 'disconnected_users', 'unsuspend -acc', 'suspend -u -r', 'suspend -u -t', 'remove -s', 'check -s', 'suspend -acc', 'delete -acc', 'delete -all -r', 'delete -s -r', 'delete -a -msg', 'create -acc', 'create -u -s', 'create -u -r', 'send -msg', 'bot -m', 'acc -c -s', 'chg -u', 'chg -p', 'user_messages/', 'server_info', 'user_rooms', 'users_photo', 'users', 'usersn', 'rooms', 'users_rooms', 'last_messages', 'cmds']

readline.set_completer_delims(' \t\n')
readline.parse_and_bind("tab: complete")

def complete(text, state):
    options = [command for command in available_commands if command.startswith(text)]
    return options[state] if state < len(options) else None

readline.set_completer(complete)

def restart_script():
    python = sys.executable
    os.execl(python, python, * sys.argv)

api_url = "https://neauapp.pagekite.me/api/"

def make_api_request(api_key, endpoint, data=None):
    headers = {'X-API-Key': api_key}
    url = f'{api_url}{endpoint}'

    while True:
        try:
            loading_animation()
            if data is not None:
                response = requests.post(url, headers=headers, json=data)
            else:
                response = requests.get(url, headers=headers)

            response.raise_for_status()

            return response
        except requests.exceptions.RequestException as e:
            if isinstance(e, requests.exceptions.ConnectionError) and "Connection refused" in str(e):
                print("\nError: The server is not available. Trying again in 3 seconds... Press (ctrl + c) to cancel.")
            elif isinstance(e, requests.exceptions.HTTPError):
                if e.response.status_code == 404:
                    print("\033[93m\nHTTP Error 404: Route does not exist.\033[0m\n\033[92mTrying again in 3 seconds... "
                          "\033[92mPress (ctrl + c) to cancel.\033[0m\n")
                    try:
                        error_details = e.response.json()
                        print("Error Details:", error_details)
                    except ValueError:
                        print("Error details could not be parsed as JSON.")
                else:
                    print(f"\nHTTP Error: {e.response.status_code}. Trying again in 3 seconds... "
                          "Press (ctrl + c) to cancel.")
            else:
                print(f"\nOcurrió un error: {e}. Trying again in 3 seconds... Press (ctrl + c) to cancel.")

            time.sleep(3)

def loading_animation():
    print("\nLoading ", end='', flush=True)

    pong_effect = ['|', '/', '-', '\\']
    
    num_frames = random.randint(2, 3)
    frame_delay = random.uniform(0.3, 0.5)

    for _ in range(num_frames):
        for char in pong_effect:
            print(char, end='', flush=True)
            time.sleep(frame_delay)
            print('\b', end='', flush=True)

    print(" " * 10, end='', flush=True)
    print("\033[G", end='', flush=True)

def show_help():
    red = "\033[91m"
    green = "\033[92m"
    reset = "\033[0m"

    print(f"{red}\nWelcome to NeauApp Help!\n")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta")
    print(f"{reset}- beta: beta\n")

def show_available_commands():
    red = "\033[91m"
    green = "\033[92m"
    reset = "\033[0m"

    print(f"{red}\n• Available Commands:\n")
    print(f"{green}- ping:{reset} Establish connection if available")
    print(f"{green}- cmds:{reset} Show list of commands")
    print(f"{green}- commands:{reset} Show list of commands")
    print(f"{green}- date:{reset} View date local")
    print(f"{green}- path:{reset} Change the request path")
    print(f"{green}- echo $PATH:{reset} View request path")
    print(f"{green}- create -acc:{reset} Create account random")
    print(f"{green}- acc -c -s:{reset} Create a specific user account")
    print(f"{green}- chg -u:{reset} Change account username")
    print(f"{green}- chg -p:{reset} Change account password")
    print(f"{green}- remove -s:{reset} Remove suspension temporaly to a user (using his username)")
    print(f"{green}- check -s:{reset} Show account status (suspension)")
    print(f"{green}- suspend -u -r:{reset} Suspend user temporarily (in time)")
    print(f"{green}- delete -all -r:{reset} Delete all existing rooms of an account (using your username)")
    print(f"{green}- delete -s -r:{reset} Delete rooms from an account (specifying room names and account)")
    print(f"{green}- bot -m:{reset} Send message every certain time (to be specified during the process)")
    print(f"{green}- delete -a -msg:{reset} Delete all messages in a room (irreversible action)")
    print(f"{green}- send -msg:{reset} Send messages to a room, (it is not necessary to enter a username from the database).")
    print(f"{green}- create -u -s:{reset} Create rooms to an account using your username")
    print(f"{green}- create -u -r:{reset} Create room to an account using your username")
    print(f"{green}- server_info:{reset} View hosting server information")
    print(f"{green}- last_messages:{reset} Show last message of each user (all rooms)")
    print(f"{green}- users_rooms:{reset} Show number of existing rooms on the server (of all users)")
    print(f"{green}- rooms:{reset} Show existing rooms on the server (regardless of users)")
    print(f"{green}- usersn:{reset} Usernames (without passwords in the Server)")
    print(f"{green}- users:{reset} Usernames (with passwords in the Server)")
    print(f"{green}- users_photo:{reset} List of all existing users with or without profile picture")
    print(f"{green}- user_rooms/{{username}}:{reset} Filter and search by name, all existing rooms of a user")
    print(f"{green}- cls:{reset} Delete history completely (without displaying list of commands)")
    print(f"{green}- sv.o:{reset} Open browser web default")
    print(f"{green}- unsuspend -acc:{reset} Unsuspend a user account using its username")
    print(f"{green}- suspend -acc:{reset} Suspend user account using your username")
    print(f"{green}- suspend -u -t:{reset} Suspend an user for time specific")
    print(f"{green}- delete -acc (username):{reset} Delete user account (using your username)")
    print(f"{green}- user_messages/{{username}}:{reset} Filter and search by name, all existing messages from a user\n")
    print(f"SHORTCUTS KEYS:\n")
    print(f"Up Arrow: Show history of sent (most recent)")
    print(f"Down Arrow: Show history of sent (older)")
    print(f"CTRL + L: Delete history (logs) completely")
    print(f"CTRL + C: Quit of terminal NeauApp\n")

def translate(input_text):
    translator = Translator()
    try:
        word_to_translate = input_text.split('"')[1]
        
        translation = translator.translate(word_to_translate, dest='es')

        print(f"\nTranslation: {translation.text}\n")

    except IndexError:
        print("\n\033[91mInvalid syntax. Use: translate \"word\"\033[0m\n")

def clear_screen():
    os.system('clear' if os.name == 'posix' else 'cls')

def open_browser(url):
    webbrowser.open(url)

def delete_account(api_key, user_input):
    delete_url = "https://neauapp.pagekite.me/api/delete_account/"
    delete_command = f'curl -X DELETE -H "X-API-Key: {api0233929329420819_key}" {delete_url}{user_input}'
    os.system(delete_command)

api0233929329420819_key = "mfk4TRF0A10sV1B4YsCdwio7BEzYKh2BNJJEgFbDx6BbOpStpQvpGE7vYk0xLsmWwlqAMken3b69PjsKw00qJ2ybjuJnRwyqKRTK1dV"

def main():
    parser = argparse.ArgumentParser(description='Script to make API requests to neauapp.py')

    parser.add_argument('endpoint', nargs='*', help='The endpoint to append after /api/')
    parser.add_argument('--list-commands', action='store_true', help='Show available commands')

    args = parser.parse_args()

    if args.list_commands:
        show_available_commands()
        return

    endpoint = ' '.join(args.endpoint)

    api_key = 'mrr33ifi3mfosmw02msndjj34rg9jwsooodmm40dnrffFFjnsjNcSndWWcz038f23994'

    if not endpoint:
        print("\033[91m" + """⠀⠀⠀⠀⠀                                
                  ⣶⣀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣀⣴⠆⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢯⣿⣲⣄⠀⠀⠀⠀⠀⠀⠀⠀⡀⠀⠀⠀⠀⠀⠀⠀⠀⣠⣴⣿⣿⠋⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠘⣟⣽⢟⣕⢄⠀⠀⠀⠀⠀⠀⣧⠀⡀⠀⠀⠀⠀⢠⢮⡾⣽⡻⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⡿⣮⣟⡼⡌⡆⠀⠀⠀⠀⡰⡵⠰⡃⠀⠀⠀⢠⢃⡻⣜⢯⣻⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⡿⣮⡵⣫⡵⢹⠀⠀⠀⠻⡄⡧⣈⠚⠀⠀⠀⢸⢺⡗⣭⣛⢿⣇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⣿⡿⡵⢞⣫⡆⡹⠀⠀⠀⢑⠥⡨⡐⠫⣢⠀⠀⢸⢺⣽⢚⡭⣯⣿⣆⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣀⣴⣿⣿⣶⣻⡭⣷⢣⠇⠄⠤⢀⠼⣄⣸⡌⡆⢠⡧⠀⠈⡷⣮⢯⣛⣶⣿⣿⣷⣄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⠀⠀⠀
⠀⠀⠈⠢⡀⠠⡒⠀⠂⠐⠀⠂⠀⣀⣴⢾⣿⣿⣿⣷⣚⣷⡿⣳⠛⠒⠒⠒⢇⠏⡚⠓⠈⢀⢬⠓⠒⠒⠚⢞⡯⣟⣶⣛⣿⣿⣿⣿⡦⣖⠀⠀⠀⠀⠂⠐⠀⡄⠀⠐⠁⠀⠀⠀
⠀⠀⠀⠀⠘⡄⠈⠢⡀⢀⣠⡴⣟⢿⣹⢿⣺⣿⣟⣶⣛⡭⠛⠁⠀⠀⠀⠀⠈⣑⣜⡆⢔⣕⣁⠀⠀⠀⠀⠀⠙⢯⡞⣛⣾⣿⣿⣸⣿⣹⣿⠶⣤⡀⠀⡠⠊⢀⠎⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠈⣦⡴⣾⢯⡽⢾⡹⣾⣝⣾⣟⠫⠞⠋⡁⠤⠀⠒⠀⠉⠁⠀⠀⠀⢈⣷⣁⠀⠀⠀⠀⠉⠁⠐⠂⠤⢈⡙⠛⠯⣻⣾⣷⣏⢾⣻⢫⡽⣻⠶⣤⡂⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⣾⣯⣷⣯⣻⣿⣧⣿⣟⡕⢋⢠⠐⠊⠁⠀⡀⣤⢀⣲⣦⣭⣥⣤⣴⣶⣤⣴⣦⣤⣬⣭⣥⣖⣂⣤⣄⡀⠀⠁⠂⡄⡉⢪⣟⣿⣵⣯⣾⣭⣟⣏⣿⡄⠀⠀⠀⠀⠀
⠀⠀⠀⠀⢸⢿⣿⣿⣿⣯⣿⣿⢳⣾⠇⠋⢀⢠⠰⠘⢃⣡⣾⣿⣿⢿⢹⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⢻⣿⣿⣷⣮⣁⠃⠶⡄⡀⠁⠳⢹⣏⣿⣟⣿⣿⣾⣿⣿⣇⠀⠀⠀⠀⠀
⠀⠀⠀⠀⢸⣟⢟⢿⣝⣟⣻⢻⢿⠁⢀⠜⠋⠀⠀⣠⣿⣿⠏⣿⣧⡇⣸⣿⣟⣯⡿⣽⣻⡿⣽⣿⣏⢈⣼⣿⡟⣧⣝⢧⡀⠀⠁⠃⡄⠀⡏⡿⣻⣻⣻⡽⣫⢻⣿⠀⠀⠀⠀⠀
⠀⠀⠀⠀⢸⣿⢼⣱⢬⣙⡻⠭⣯⣦⣀⠑⠄⣀⣼⣿⣿⣮⠃⢿⣻⡿⣿⠟⣾⢷⣻⢯⣷⣟⣿⡻⣿⣿⣟⣿⠃⡾⣿⣷⡵⣄⢀⠔⢁⣠⣷⠿⢝⡚⡭⢮⣹⢿⡇⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⢿⣾⣹⢾⡱⣺⠭⣽⣱⢞⡿⣩⢿⣟⣳⣿⢿⣿⣿⣿⡽⡍⢸⣟⣯⣟⣿⢾⡽⣾⡇⠙⣺⣽⣿⣷⣿⣿⣷⢻⣷⣭⢻⣗⢦⣻⡱⣽⢚⣟⣦⣿⣿⠃⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⡸⢿⣿⣟⣧⣷⣹⢥⠷⣞⣱⢏⡾⣱⣎⠧⣽⡱⠯⣟⢿⡡⠈⣿⣳⢿⡾⣿⡽⣷⠃⢄⡧⣟⡝⡧⢿⣲⣙⣧⢳⡞⣧⠺⡭⣖⢿⣸⣏⣷⣿⣿⠏⠀⠀⠀⠀⠀⠀
⠀⠀⠀⢀⠜⠀⠠⠛⠿⣿⣿⣿⣿⣿⣵⣯⣾⢾⡳⣌⣿⢣⣝⣟⢣⠗⣝⢷⣿⣟⣯⣟⡷⣿⣿⡶⣫⣚⢖⡻⣵⣋⠷⣞⠼⣯⣳⣽⣯⣿⣿⣿⣿⣿⠿⠛⢅⠀⠑⡀⠀⠀⠀⠀
⠀⠀⢀⠎⠀⡰⠁⠀⠀⠀⠈⠉⠛⣿⣿⣿⣿⣷⣿⣋⣮⢷⡹⣌⣧⢿⢫⢵⣻⣟⣾⣽⣻⢷⡿⡽⣜⢻⢮⣕⢫⢷⣽⣎⣿⣿⣿⣿⣿⡿⡟⠉⠉⠀⠀⠀⠀⢢⠀⠘⠄⠀⠀⠀
⠀⢀⠊⠀⡐⠀⠀⢀⣀⠀⠀⠀⢸⣿⣾⣿⣿⣿⣿⣿⣾⡷⢻⡹⣜⣣⣿⢫⢧⣿⣟⣾⣽⣿⢻⣞⣧⣏⡳⢯⣛⢾⣶⣿⣿⣿⣿⣿⣿⡇⢻⠀⠀⠀⢀⣀⠀⠀⠡⠀⠈⡄⠀⠀
⠀⠌⠀⡰⠀⠀⠀⢸⣿⣷⣤⣀⠘⣿⣿⣿⣿⣿⣿⣽⣷⣿⣿⣿⣭⣷⣼⣟⣾⣻⣿⣯⢿⣏⣿⣿⣶⣾⣽⣻⣟⣿⣻⣿⣽⣿⣿⣿⣿⣇⡏⢀⣤⣴⡿⡝⠀⠀⠀⢣⠀⠘⡀⠀
⠐⠀⢠⠁⠀⠀⠀⠀⠙⣷⣿⣻⣷⣿⣿⣿⣻⣟⣿⣯⣿⣿⣽⣯⣟⣭⣷⣿⣾⡿⣯⣿⢿⣿⣷⣿⣿⣼⣹⣿⣻⣿⣿⣽⣿⢿⣻⣽⣿⣿⢳⣿⣟⣟⠟⠀⠀⠀⠀⠀⠆⠀⢡⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⣿⣷⣟⣿⣽⣿⣯⣷⣿⡾⣿⣶⣯⣟⠿⣟⣿⣻⣽⢿⣽⣻⣿⣻⣾⣳⢯⣟⣿⣻⣿⣿⣟⣿⣭⣛⣿⣳⣯⣿⣏⣾⣟⣾⣿⠀⠀⠀⠀⠀⠀⠘⡀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⣿⣿⢿⣿⣿⣟⣿⢿⣯⣟⣷⣻⣾⣽⣻⣾⡿⣷⣿⣻⣾⢿⣷⣿⢿⣻⣿⣻⣿⢿⣻⣾⣽⣾⣽⣻⣽⡿⣿⢷⣽⣿⣿⣿⢹⠀⠀⠀⠀⠀⠀⠀⠃⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠹⣿⣟⣿⣿⣿⣯⣿⣟⣿⣿⣿⣷⣿⣻⣾⣽⢿⣽⣻⢾⡿⣯⢿⣻⣽⢯⡿⣽⡻⣫⣵⣾⣾⣿⣟⣿⣿⢿⡟⣾⣿⣟⣿⡞⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠹⣿⣻⣽⣿⣯⣟⣿⣿⣿⡿⠟⢻⠟⡿⣾⣭⣽⣿⣽⣿⣿⣿⣿⣿⣿⣿⣿⣿⠟⠟⢛⠿⣿⣿⣿⣿⣿⢸⣿⡿⣿⡞⠀⠀⠀⠀⠀⠀⠀⠀⠘⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢹⣿⢿⣿⣟⣿⣿⣿⣿⠀⠀⢼⠠⠌⠘⣿⣿⣿⣿⡿⣿⣟⢿⣿⣿⣿⡋⠀⠄⡤⠄⠈⣿⣿⣿⣿⣼⢸⣿⣿⢻⠀⠀⠀⠀⠀⠀⠀⠀⠀⢘⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣾⣿⣿⣿⣿⣻⣿⣿⣿⣿⣶⣶⣶⣶⣿⣿⣿⣿⣿⢿⣻⣯⣸⣷⣿⣿⣿⣷⣶⣷⣶⣾⣿⣿⣿⣿⢿⣾⣿⣿⣾⠀⠀⠀⠀⠀⠀⠀⠀⠀⠘⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠹⢿⣿⣿⢷⣿⣿⣿⣯⡿⢷⣿⣿⣿⣿⣿⣻⣷⣿⣿⣿⣿⣞⣿⣻⣽⢿⣿⣿⣷⣿⣟⣫⣿⣿⣿⣿⣷⡌⣻⠟⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠠
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢿⣿⣯⣿⣳⣿⣽⣻⣿⣻⡽⣟⣾⣳⣿⣿⣿⣿⣿⣿⣿⣷⢿⣿⣻⢾⣻⣟⡿⣿⡯⢿⣾⣿⣵⣿⡣⠃⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⢀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠙⢿⣿⣿⣿⣿⣿⣿⣿⣯⣷⡿⣿⣿⣿⣿⣿⣿⣿⣿⡾⣟⣯⣯⣴⣿⣿⣿⣿⣿⣿⣿⠎⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠸⠀⠀⠀
⠀⠀⠈⠆⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⡠⠊⣿⣿⣿⣿⣿⣿⣿⡾⣟⣿⣿⣿⣿⣿⣿⣿⣿⣷⣿⣿⣿⣿⣿⣿⣿⣿⣿⡉⠢⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⠃⠀⠄⠀
⠀⠀⠀⠘⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠠⠊⠠⠈⠈⣿⣷⣿⢻⣷⣿⣿⢿⣻⣿⡿⣿⣿⢿⣿⣻⣷⣿⡻⣿⡿⡏⣿⣷⣿⠃⠑⢄⠐⢄⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⠎⠀⡰⠀⠀
⠀⠀⢢⠀⠘⡀⠀⠀⠀⠀⠀⠀⡠⠐⢀⠔⠁⠀⠀⢸⣿⣿⣼⠂⢻⠃⣿⢻⣷⣿⣿⣾⣿⡟⣿⡟⢿⠋⣿⠁⣸⣿⣿⣿⠀⠀⠀⠑⠄⠑⢄⠀⠀⠀⠀⠀⠀⢀⠎⠀⡰⠁⠀⠀
⠀⠀⠀⠡⡀⠈⢄⠀⢀⡠⠔⠊⠀⠀⠆⠀⠀⠀⠀⢸⣿⣿⣿⣷⣿⠀⣯⠀⡿⢹⠛⣿⠟⣷⣿⠃⣾⡄⠙⣶⣿⣿⣽⣿⠀⠀⠀⠀⠈⡄⠀⠈⠂⠄⣀⠀⢠⠊⠀⡐⠁⠀⠀⠀
⠀⠀⠀⠀⠑⡀⠀⠪⡉⠉⠉⠉⠉⠉⠁⠀⠀⠀⠀⠘⣿⣿⢿⣿⢧⡚⣿⣤⡇⡸⠀⢿⠀⢹⣿⣦⣿⡇⣿⣿⣿⣿⣾⠇⠀⠀⠀⡀⠈⠉⠉⠉⠉⠉⠉⡙⠁⢀⠜⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠘⢆⠀⠘⢀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢸⣿⣿⣧⢿⣿⣿⣿⣿⣷⣦⣿⣤⣾⣿⣿⣿⣿⡿⡜⣿⣷⡟⠀⠀⣴⣿⣿⣿⣶⡄⠀⠀⣠⠞⠀⣠⠆⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠈⠳⡄⠈⠃⠀⠀⣤⣤⡄⢠⠀⢠⡄⢨⣿⡿⣿⣯⠹⠻⣿⣿⣿⣿⣿⣿⢿⡿⣿⡿⣿⣽⣾⣿⢻⢧⣤⣼⣿⣵⣦⢨⣿⣿⣤⠞⠁⠀⠞⠁⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠈⠢⡀⠀⠐⢌⡉⠐⠢⡀⠀⠀⢰⠹⢿⣻⢿⣸⣄⢹⡻⢿⣿⣿⣿⡿⣿⣜⢿⣞⣿⣿⣳⠏⠉⠀⠀⠙⣿⠟⠀⣹⡇⡇⢀⠔⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠑⢄⡀⠈⠂⠄⡀⠑⠄⠘⠴⠉⣿⣟⣿⣧⣼⣧⣸⡆⣼⢀⣿⣿⣟⣧⡻⣿⣿⣷⣦⡰⠀⡠⠊⡠⡶⠈⣾⣿⠗⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠒⠄⡀⠀⠁⠂⠆⠀⢌⠈⣿⣯⢿⡽⣯⣿⢿⡿⣾⣟⣿⣿⢿⣻⣮⣿⣾⡿⣦⣘⠂⠁⠀⣠⣾⡿⡟⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⣀⡀⢀⡀⠀⠀⠀⠀⠁⠂⡄⢀⡀⠀⠁⠐⠛⠻⢽⣳⣟⣯⣟⣷⣻⣾⣽⠿⢿⣿⣞⣯⢿⡿⣿⣻⣿⢿⣟⢿⡿⠁⣀⠀⣀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⡠⠊⠀⠀⠀⠈⡆⠀⠀⠀⢀⠎⢠⠂⠈⠑⡀⠠⡀⠤⠤⠀⠀⠀⠀⠀⠀⠀⠠⠤⠄⢘⠙⠻⠯⢿⣟⣷⣯⡿⠾⠋⢀⠊⠀⠀⠀⠈⢢⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⢠⠁⠀⢠⠊⠀⠈⠃⠀⠀⢀⠂⡠⠁⠀⠀⠀⠈⢄⠐⠄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⡠⠁⡰⠁⠀⠀⠀⢢⠈⢄⠀⠀⠈⠊⠀⠁⠂⠀⠀⡇⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠈⡄⠀⠘⢄⠀⠀⠀⢀⠠⠁⡐⠁⠀⠀⠀⠀⠀⠈⢂⠈⢄⠀⠀⠀⠀⠀⠀⠀⠀⡐⠁⠔⠀⠀⠀⠀⠀⠀⠡⡀⠢⡀⠀⠀⠀⢀⠄⠀⠀⠇⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠐⢄⠀⠀⠉⠐⠂⠁⠀⠌⠀⠀⠀⠀⠀⠀⠀⠀⠀⠣⠀⠢⠀⠀⠀⠀⠀⢀⠌⢀⠌⠀⠀⠀⠀⠀⠀⠀⠀⠑⢄⠀⠁⠒⠈⠀⠀⢀⠌⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠁⠂⠠⠄⠐⠊⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠱⡀⠡⡀⠀⠀⢠⠊⢀⠂⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠁⠒⠀⠄⠀⠂⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠐⠄⠐⠄⡠⠁⡠⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢆⠈⠀⡐⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢢⠌⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀\n""" + "\033[0m")
        print("NeauApp 1.0.13 (snapshot, API Nov 13 2023, 13:31:09)\n[G++ 1.0.3] on linux Rhel 7")
        print('Type "help", or "commands" for more information.\n')

        history = []

        api_url = "https://neauapp.pagekite.me/api/"

        try:
            while True:
                hora_actual = datetime.now().strftime("%H:%M")
                try:
                    user_input = input(f'⚒️ {hora_actual} admin/api ~ > ')
                except EOFError:
                    print("\nCtrl + D detected. Exiting NeauApp. Goodbye!")
                    break

                if not user_input:
                    continue

                history.append(user_input)

                try:
                    if user_input.lower() == 'exit':
                        print("\nExiting NeauApp. Goodbye!")
                        break
                    elif user_input.lower() == 'path':
                        choice = input("\nDo you want to use the test URL (localhost)? (Y/n): ")
                        if choice.lower() == 'y':
                            if api_url == "http://127.0.0.1:5000/api/":
                                print("\n\033[91mPath is already set to localhost. No changes made.\033[0m\n")
                            else:
                                api_url = "http://127.0.0.1:5000/api/"
                                print("\n\033[92mUsing test URL: localhost:5000\033[0m\n")
                        elif choice.lower() == 'n':
                            if api_url == "https://neauapp.pagekite.me/api/":
                                print("\n\033[91mPath is already set to default. No changes made.\033[0m\n")
                            else:
                                api_url = "https://neauapp.pagekite.me/api/"
                                print("\n\033[93mUsing default URL: neauapp.pagekite.me\033[0m\n")
                        else:
                            print("\nInvalid choice. Please enter 'Y' or 'N'.\n")
                    elif user_input.lower().startswith('path '):
                        if len(user_input.split()) > 2:
                            print("\nInvalid usage of arguments. Please use either -y or -n, not both or mixed.\n")
                        else:
                            arg = user_input.lower().split()[1]
                            if arg == '-y':
                                if api_url == "http://127.0.0.1:5000/api/":
                                    print("\n\033[91mPath is already set to localhost. No changes made.\033[0m\n")
                                else:
                                    api_url = "http://127.0.0.1:5000/api/"
                                    print("\n\033[92mPath changed successfully to localhost:5000\033[0m\n")
                            elif arg == '-n':
                                if api_url == "https://neauapp.pagekite.me/api/":
                                    print("\n\033[91mPath is already set to default. No changes made.\033[0m\n")
                                else:
                                    api_url = "https://neauapp.pagekite.me/api/"
                                    print("\n\033[93mPath changed successfully to neauapp.pagekite.me\033[0m\n")
                            else:
                                choice = input("\nDo you want to use the test URL (localhost)? (Y/n): ")
                                if choice.lower() == 'y':
                                    api_url = "http://127.0.0.1:5000/api/"
                                    print("\n\033[92mUsing test URL: localhost:5000\033[0m\n")
                                else:
                                    api_url = "https://neauapp.pagekite.me/api/"
                                    print("\n\033[93mUsing default URL: neauapp.pagekite.me\033[0m\n")
                    elif user_input.lower() == 'echo $path':
                        if api_url == "https://neauapp.pagekite.me/api/":
                            print("\nwww/http/server.default\n")
                        elif api_url == "http://127.0.0.1:5000/api/":
                            print("\nlocalhost:running\n")
                        else:
                            print("\nUnknown\n")
                    elif user_input.lower() == 'neauapp':
                        print("\nRestarting NeauApp...")
                        clear_screen()
                        restart_script()
                    elif user_input.lower() == 'sv.o':
                        print("\nOpening a browser...\n")
                        open_browser("https://google.com")
                    elif user_input.lower() == 'commands' or user_input.lower() == 'cmds':
                        show_available_commands()
                    elif user_input.lower() == 'help':
                        show_help()
                    elif user_input.lower() == 'clear':
                        clear_screen()
                        show_available_commands()
                    elif user_input.lower() == 'cls':
                        clear_screen()
                        print()
                    elif user_input.lower() == 'date':
                        current_date = datetime.now().strftime("%Y-%m-%d %A")
                        print(f"\nCurrent date: {current_date}\n")
                    elif user_input.lower().startswith('translate'):
                        translate(user_input)
                    elif user_input.lower() == 'acc -c -s':
                        username = input("\nEnter the desired username: ")
                        password = input("Enter the desired password: ")

                        api_url = "https://neauapp.pagekite.me/api/create_account_specific"
                        headers = {
                            "Content-Type": "application/json",
                            "Authorization": "es7S80Apak3V866h6kjpNFk2sXciYfBy"
                        }
                        payload = {
                            "username": username,
                            "password": password
                        }

                        response = requests.post(api_url, json=payload, headers=headers)

                        if response.status_code == 200:
                            print("\n\033[92mAccount created successfully.\033[0m")
                        else:
                            print(f"\n\033[91mError creating account. Status code: {response.status_code}\033[0m\n")
                            print(response.text)
                    elif user_input.lower() == 'create -acc':
                        while True:
                            try:
                                count = int(input("\nEnter the number of accounts to create: "))
                                break
                            except ValueError:
                                print("\n\033[91mError: Please enter a valid number.\033[0m")

                        api_url = "https://neauapp.pagekite.me/api/create_accounts"
                        headers = {
                            "Content-Type": "application/json",
                            "Authorization": "es7S80Apak3V866h6kjpNFk2sXciYfBy"
                        }
                        params = {
                            "count": count
                        }

                        response = requests.post(api_url, params=params, headers=headers)

                        if response.status_code == 200:
                            accounts = response.text
                            print(f"\n\033[92mSuccessfully created {count} account(s):\033[0m\n\n{accounts}")
                        else:
                            print(f"\n\033[91mError creating accounts. Status code: {response.status_code}\033[0m\n")
                            print(response.text)
                    elif user_input.lower().startswith('delete -acc '):
                        account_info = urllib.parse.quote(user_input[len('delete -acc '):])
                        delete_account(api_key, account_info)
                    elif user_input.lower() == 'chg -u':
                        while True:
                            old_username = input("\nEnter the current username: ")

                            if 3 <= len(old_username) <= 14:
                                break
                            else:
                                print("\n\033[91mError: The current user name must be between 3 and 14 characters.\033[0m")

                        while True:
                            new_username = input("\nEnter the new username: ")

                            if 3 <= len(new_username) <= 14 and new_username != old_username:
                                break
                            elif new_username == old_username:
                                print("\n\033[93mFailed!: The new user name cannot be the same as the current user name.\033[0m")
                            else:
                                print("\n\033[91mError: The new username must be between 3 and 14 characters.\033[0m")

                        api_url = "https://neauapp.pagekite.me/api/update_profile"
                        headers = {
                            "Content-Type": "application/json",
                            "Authorization": "es7S80Apak3V866h6kjpNFk2sXciYfBy"
                        }
                        payload = {
                            "target_username": old_username,
                            "new_username": new_username
                        }

                        response = requests.post(api_url, json=payload, headers=headers)

                        if response.status_code == 200:
                            print(f"\n\033[92mUsername successfully changed from {old_username} to {new_username}.\033[0m\n")
                        else:
                            print(f"\n\033[91mError changing username. Status code: {response.status_code}\033[0m\n")
                            print(response.text)
                    elif user_input.lower() == 'chg -p':
                        target_username = input("\nEnter the username for which you want to change the password: ")

                        while True:
                            new_password = input("\nEnter the new password: ")

                            if 6 <= len(new_password) <= 16:
                                break
                            else:
                                print("\n\033[91mError: The password must be between 6 and 16 characters.\033[0m")

                        api_url = "https://neauapp.pagekite.me/api/update_profile"
                        headers = {
                            "Content-Type": "application/json",
                            "Authorization": "es7S80Apak3V866h6kjpNFk2sXciYfBy"
                        }
                        payload = {
                            "target_username": target_username,
                            "new_password": new_password
                        }

                        response = requests.post(api_url, json=payload, headers=headers)

                        if response.status_code == 200:
                            print(f"\n\033[92mPassword successfully changed for {target_username}.\033[0m\n")
                        else:
                            print(f"\n\033[91mError changing password. Status code: {response.status_code}\033[0m\n")
                            print(response.text)
                    elif user_input.lower() == 'create -u -s':
                        username = input("\nEnter the desired username: ")
                        num_rooms = int(input("Enter the number of rooms: "))
                        room_name = input("Enter the room name: ")

                        api_url = f"https://neauapp.pagekite.me/api/create_user_rooms/{username}/{num_rooms}/{room_name}"
                        headers = {
                            "Content-Type": "application/json",
                            "Authorization": "es7S80Apak3V866h6kjpNFk2sXciYfBy"
                        }

                        response = requests.post(api_url, headers=headers)

                        if response.status_code == 200:
                            print(f"\n\033[92m{num_rooms} rooms with the name '{room_name}' created successfully.\033[0m")
                        else:
                            print(f"\n\033[91mError creating rooms. Status code: {response.status_code}\033[0m\n")
                            print(response.text)
                    elif user_input.lower() == 'create -u -r':
                        username = input("\nEnter the desired username: ")
                        room_name = input("Enter the room name: ")

                        api_url = f"https://neauapp.pagekite.me/api/create_user_room/{username}/{room_name}"
                        headers = {
                            "Content-Type": "application/json",
                            "Authorization": "es7S80Apak3V866h6kjpNFk2sXciYfBy"
                        }

                        response = requests.post(api_url, headers=headers)

                        if response.status_code == 200:
                            print(f"\n\033[92mThe room ({room_name}) was successfully created to: '{username}'\033[0m")
                        else:
                            print(f"\n\033[91mError creating room. Status code: {response.status_code}\033[0m\n")
                            print(response.text)
                    elif user_input.lower() == 'send -msg':
                        room_id = input("\nEnter the room ID: ")
                        user_nick = input("Enter your nickname: ")
                        api_url = "https://neauapp.pagekite.me/api/send_message"
                        headers = {
                            "Content-Type": "application/json",
                            "Authorization": "es7S80Apak3V866h6kjpNFk2sXciYfBy"
                        }

                        while True:
                            message_content = input("\nEnter the message content (type 'exit' to stop): ")

                            if message_content.lower() == 'exit':
                                break

                            data = {
                                "room": room_id,
                                "message": message_content,
                                "nick": user_nick
                            }

                            response = requests.post(api_url, json=data, headers=headers)

                            if response.status_code == 200:
                                print("\n\033[92mMessage sent successfully.\033[0m")
                            else:
                                print(f"\n\033[91mError sending message. Status code: {response.status_code}\033[0m\n")
                                print(response.text)
                    elif user_input.lower() == 'bot -m':
                        room_id = input("Enter the room ID: ")
                        user_nick = input("Enter your username: ")
                        message_content = input("Enter the message to be sent periodically: ")

                        delay_response = input("Do you want to add a time delay between messages? (y/n): ")

                        if delay_response.lower() == 'y':
                            delay_time = float(input("Enter the time delay between messages (in seconds): "))
                        else:
                            delay_time = None

                        api_url = "https://neauapp.pagekite.me/api/send_message"
                        headers = {
                            "Content-Type": "application/json",
                            "Authorization": "es7S80Apak3V866h6kjpNFk2sXciYfBy"
                        }

                        data = {
                            "room": room_id,
                            "message": message_content,
                            "nick": user_nick
                        }

                        while True:
                            response = requests.post(api_url, json=data, headers=headers)

                            if response.status_code == 200:
                                random_uuid = str(uuid.uuid4())
                                print("\n\033[92mMessage sent successfully.\033[0m", f"({random_uuid})")

                                print("Room ID:", room_id)
                                print("Username:", user_nick)
                                print("Message Content:", message_content)
                                print("Timestamp:", time.strftime("%Y-%m-%d %H:%M:%S"))

                            else:
                                print(f"\n\033[91mError sending message. Status code: {response.status_code}\033[0m\n")
                                print(response.text)

                            if delay_time is not None:
                                time.sleep(delay_time)
                            else:
                                break
                    elif user_input.lower() == 'delete -a -msg':
                        message_id = input("\nEnter the room ID to delete all messages: ")
                        api_url_delete = f"https://neauapp.pagekite.me/api/delete_messages/{message_id}"
                        headers_delete = {
                            "X-API-Key": api_key
                        }

                        response_delete = requests.delete(api_url_delete, headers=headers_delete)

                        if response_delete.status_code == 200:
                            print("\n\033[92mMessage deleted successfully.\033[0m\n")
                        else:
                            print(f"\n\033[91mError deleting message. Status code: {response_delete.status_code}\033[0m\n")
                            print(response_delete.text)
                    elif user_input.lower() == 'delete -s -r':
                        username = input("\nEnter the username: ")
                        room_names = input("Enter room names (comma-separated with space): ").split(', ')

                        api_url = "https://neauapp.pagekite.me/api/delete_specific_rooms"
                        headers = {
                            "Content-Type": "application/json"
                        }

                        payload = {
                            "username": username,
                            "room_names": room_names
                        }

                        response = requests.delete(api_url, headers=headers, json=payload)

                        if response.status_code == 200:
                            print(f"\n\033[92m{response.json()['message']}\033[0m\n")
                        else:
                            print(f"\n\033[91mError deleting specific rooms. Status code: {response.status_code}\033[0m\n")
                            print(response.text)
                    elif user_input.lower() == 'delete -all -r':
                        username = input("\nEnter the username: ")
                        api_url = f"https://neauapp.pagekite.me/api/delete_rooms_by_username/{username}"
                        token = "mrr33ifi3mfosmw02msndjj34rg9jwsooodmm40dnrffFFjnsjNcSndWWcz038f23994"

                        headers = {
                            "Authorization": f"Bearer {token}"
                        }

                        response = requests.delete(api_url, headers=headers)

                        if response.status_code == 200:
                            print(f"\n\033[92m{response.json()['message']}\033[0m\n")
                        else:
                            print(f"\n\033[91mError deleting all rooms. Status code: {response.status_code}\033[0m\n")
                            print(response.text)
                    elif user_input.lower() == 'suspend -acc':
                        username_to_suspend = input("\nEnter the username to suspend: ")
                        api_url_suspend = f"https://neauapp.pagekite.me/api/suspend_user/{username_to_suspend}"
                        headers_suspend = {
                            "X-API-Key": api0233929329420819_key
                        }

                        response_suspend = requests.post(api_url_suspend, headers=headers_suspend)

                        if response_suspend.status_code == 200:
                            print("\n\033[92mUser suspended successfully.\033[0m\n")
                        else:
                            print(f"\n\033[91mError suspending user. Status code: {response_suspend.status_code}\033[0m\n")
                            print(response_suspend.text)
                    elif user_input.lower() == 'remove -s':
                        username_to_unsuspend = input("\nEnter the username to remove suspension: ")
                        api_url_unsuspend = f"https://neauapp.pagekite.me/api/remove_suspension/{username_to_unsuspend}"
                        headers_unsuspend = {
                            "X-API-Key": api0233929329420819_key
                        }

                        response_unsuspend = requests.post(api_url_unsuspend, headers=headers_unsuspend)

                        if response_unsuspend.status_code == 200:
                            print("\n\033[92mSuccessfully removed suspension.\033[0m\n")
                        else:
                            print(f"\n\033[91mError removing suspension. Status code: {response_unsuspend.status_code}\033[0m\n")
                            print(response_unsuspend.text)
                    elif user_input.lower() == 'check -s':
                        username_to_check = input("\nEnter the username to check suspension: ")
                        api_url_check_suspension = f"https://neauapp.pagekite.me/api/check_suspension/{username_to_check}"
                        headers_check_suspension = {
                            "X-API-Key": api0233929329420819_key
                        }

                        response_check_suspension = requests.get(api_url_check_suspension, headers=headers_check_suspension)

                        if response_check_suspension.status_code == 200:
                            result = response_check_suspension.json()
                            suspended_status = result["suspended"]

                            if suspended_status:
                                print("\n\033[91mUser is suspended.\033[0m\n")
                                suspension_info = result.get("suspension_info", {})
                                if suspension_info:
                                    print(f"Suspension End Time: {suspension_info.get('end_time', 'N/A')}\n")
                                    print(f"Time Remaining: {suspension_info.get('time_remaining', 'N/A')} seconds\n")
                            else:
                                print("\n\033[92mUser is not suspended.\033[0m\n")

                        else:
                            print(f"\n\033[91mError checking suspension status. Status code: {response_check_suspension.status_code}\033[0m\n")
                            print(response_check_suspension.text)
                    elif user_input.lower() == 'suspend -u -r':
                        username_to_suspend_random = input("\nEnter the username to suspend: ")
                        api_url_suspend_random = f"https://neauapp.pagekite.me/api/suspend_user_random/{username_to_suspend_random}"
                        headers_suspend_random = {
                            "X-API-Key": api0233929329420819_key
                        }

                        response_suspend_random = requests.post(api_url_suspend_random, headers=headers_suspend_random)

                        if response_suspend_random.status_code == 200:
                            result_suspend_random = response_suspend_random.json()
                            print(f"\n\033[92m{result_suspend_random['message']}\033[0m")
                            print(f"Suspension end time (UTC): {result_suspend_random['suspension_end_time_utc']}\n")
                        else:
                            print(f"\n\033[91mError suspending user. Status code: {response_suspend_random.status_code}\033[0m\n")
                            print(response_suspend_random.text)
                    elif user_input.lower() == 'suspend -u -t':
                        username_to_suspend_time = input("\nEnter the username to suspend: ")

                        while True:
                            time_format = input("Enter the time format (seconds/minutes/hours): ").lower()

                            if time_format not in ['seconds', 'minutes', 'hours']:
                                print("\n\033[91mInvalid time format.\033[0m \033[93mPlease enter 'seconds', 'minutes', or 'hours'.\033[0m\n")
                                continue

                            time_value = int(input("Enter the suspension time value: "))

                            api_url_suspend_time = f"https://neauapp.pagekite.me/api/suspend_user_time/{username_to_suspend_time}/{time_format}/{time_value}"
                            headers_suspend_time = {
                                "X-API-Key": api0233929329420819_key
                            }

                            response_suspend_time = requests.post(api_url_suspend_time, headers=headers_suspend_time)

                            if response_suspend_time.status_code == 200:
                                result_suspend_time = response_suspend_time.json()
                                print(f"\n\033[92m{result_suspend_time['message']}\033[0m")
                                print(f"Suspension end time (UTC): {result_suspend_time['suspension_end_time_utc']}\n")
                                break
                            else:
                                print(f"\n\033[91mError suspending user with time. Status code: {response_suspend_time.status_code}\033[0m\n")
                                print(response_suspend_time.text)
                    elif user_input.lower() == 'unsuspend -acc':
                        username_to_suspend = input("\nEnter the username to unsuspend: ")
                        api_url_suspend = f"https://neauapp.pagekite.me/api/unsuspend_user/{username_to_suspend}"
                        headers_suspend = {
                            "X-API-Key": api0233929329420819_key
                        }

                        response_unsus = requests.post(api_url_suspend, headers=headers_suspend)

                        if response_unsus.status_code == 200:
                            print("\n\033[92mUser unsuspended successfully.\033[0m\n")
                        else:
                            print(f"\n\033[91mError removing user suspension. Status code: {response_unsus.status_code}\033[0m\n")
                            print(response_unsus.text)
                    else:
                        response = make_api_request(api_key, user_input)
                        print(response.status_code)
                        print(response.text)
                except KeyboardInterrupt:
                    print("\033[91m\nCommand execution interrupted. Stopping execution...\n\033[0m")

        except KeyboardInterrupt:
            print("\nCtrl + C detected. Exiting NeauApp. Goodbye!")

if __name__ == '__main__':
    main()
