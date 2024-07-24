# Sistemas-Base-de-administra-o---Samp
Sistemas para GM base do underground divulgada pelo  lehsamp, código adaptável.

Sistemas Disponíveis:

- GMX: Reinicia o servidor.
- Kick: Expulsa um jogador do servidor.
- Banimento: Bane um jogador do servidor.
- Listar Plugins: Exibe a lista de plugins carregados no servidor.
- Recarregar FS: Recarrega um filtro script (FS) no servidor.
- Descarregar FS: Remove um filtro script (FS) do servidor.
- Listar Bans: Mostra a lista de jogadores banidos.
- Trancar o Servidor: Define uma nova senha para o servidor.

Observações:

- O código é baseado na Gamemode do Underground do LehSAMP e utiliza permissões de administrador dos níveis 3 a 10.
- Os comandos são enviados diretamente ao RCON do servidor, dispensando a necessidade de estar logado no RCON. Por exemplo, em vez de usar /rcon ban (ID), você pode usar /ban (CPF) (identificador fixo da GM base do Underground).

Código desenvolvido por mim com auxílio do ChatGPT 3.5 :)

CMD:ban(playerid, params[]) {

    new id, reason[128];

    if(Logado[playerid] == true) {

        if(pInfo[playerid][Admin] < 6 || pInfo[playerid][Admin] > 10) {

            return SendClientMessage(playerid, -1, "{C0C0C0}Comando restrito a administradores de nível 6 a 10");

        }

        if(sscanf(params, "ds[128]", id, reason)) {

            SendClientMessage(playerid, -1, "{C0C0C0}Modo de uso: /ban [ CPF ] [ motivo ]");

            return 1;

        } else {

            foreach(new i: Player) {

                if(Logado[i] == true && pInfo[i][IDf] == id) {

                    new name[30];

                    GetPlayerName(i, name, sizeof(name));

                    new command[200];

                    format(command, sizeof(command), "ban %d %s", i, reason);

                    SendRconCommand(command);

                    return 1;

                }

            }

            SendClientMessage(playerid, -1, "{C0C0C0}Nenhum jogador encontrado com o CPF especificado.");

        }

    }

    return 1;

}



CMD:kick(playerid, params[]) {

    new id, reason[128];

    if(Logado[playerid] == true) {

        if(pInfo[playerid][Admin] < 6 || pInfo[playerid][Admin] > 10) {

            return SendClientMessage(playerid, -1, "{C0C0C0}Comando restrito a administradores de nível 6 a 10");

        }

        if(sscanf(params, "ds[128]", id, reason)) {

            SendClientMessage(playerid, -1, "{C0C0C0}Modo de uso: /kick [ CPF ] [ motivo ]");

            return 1;

        } else {

            foreach(new i: Player) {

                if(Logado[i] == true && pInfo[i][IDf] == id) {

                    new name[30];

                    GetPlayerName(i, name, sizeof(name));

                    new command[200];

                    format(command, sizeof(command), "kick %d %s", i, reason);

                    SendRconCommand(command);

                    return 1;

                }

            }

            SendClientMessage(playerid, -1, "{C0C0C0}Nenhum jogador encontrado com o CPF especificado.");

        }

    }

    return 1;

}



CMD:gmx(playerid) {

    if(Logado[playerid] == true) {

        if(pInfo[playerid][Admin] < 6 || pInfo[playerid][Admin] > 10) {

            return SendClientMessage(playerid, -1, "{C0C0C0}Comando restrito a administradores de nível 6 a 10");

        }

        SendRconCommand("gmx");

    }

    return 1;

}



CMD:unban(playerid, params[]) {

    new name[30], reason[128];

    if(Logado[playerid] == true) {

        if(pInfo[playerid][Admin] < 5 || pInfo[playerid][Admin] > 10) {

            return SendClientMessage(playerid, -1, "{C0C0C0}Comando restrito a administradores de nível 5 a 10");

        }

        if(sscanf(params, "s[30]s[128]", name, reason)) {

            SendClientMessage(playerid, -1, "{C0C0C0}Modo de uso: /unban [ Nickname ] [ motivo ]");

            return 1;

        } else {

            new command[200];

            format(command, sizeof(command), "unban %s", name);

            SendRconCommand(command);

            new adminName[30];

            GetPlayerName(playerid, adminName, sizeof(adminName));

            new msg[200];

            format(msg, sizeof(msg), "{FF00CC}Admin | {FFFFFF}%s{FF00CC} desbaniu o jogador {FFFFFF}%s{FF00CC} pelo motivo: {FFFFFF}%s{FF00CC}.", adminName, name, reason);

            SendClientMessageToAll(-1, msg);

        }

    }

    return 1;

}



CMD:allmsg(playerid, params[]) {

    new mensagem[128];

    if(Logado[playerid] == true) {

        if(pInfo[playerid][Admin] < 6 || pInfo[playerid][Admin] > 10) {

            return SendClientMessage(playerid, -1, "{C0C0C0}Comando restrito a administradores de nível 6 a 10");

        }

        if(sscanf(params, "s[128]", mensagem)) {

            SendClientMessage(playerid, -1, "{C0C0C0}Modo de uso: /dizer [ mensagem ]");

            return 1;

        } else {

            new command[200];

            format(command, sizeof(command), "say %s", mensagem);

            SendRconCommand(command);

        }

    }

    return 1;

}



CMD:recarregarbans(playerid) {

    if(Logado[playerid] == true) {

        if(pInfo[playerid][Admin] < 6 || pInfo[playerid][Admin] > 10) {

            return SendClientMessage(playerid, -1, "{C0C0C0}Comando restrito a administradores de nível 6 a 10");

        }

        SendRconCommand("reloadbans");

        SendClientMessage(playerid, -1, "{FF00CC}Bans recarregados com sucesso.");

    }

    return 1;

}



CMD:plugins(playerid) {

    if(Logado[playerid] == true) {

        if(pInfo[playerid][Admin] < 6 || pInfo[playerid][Admin] > 10) {

            return SendClientMessage(playerid, -1, "{C0C0C0}Comando restrito a administradores de nível 6 a 10");

        }

        SendRconCommand("plugins");

    }

    return 1;

}



CMD:descarregarfs(playerid, params[]) {

    new fs[128];

    if(Logado[playerid] == true) {

        if(pInfo[playerid][Admin] < 6 || pInfo[playerid][Admin] > 10) {

            return SendClientMessage(playerid, -1, "{C0C0C0}Comando restrito a administradores de nível 6 a 10");

        }

        if(sscanf(params, "s[128]", fs)) {

            SendClientMessage(playerid, -1, "{C0C0C0}Modo de uso: /descarregarfs [ nome_fs ]");

            return 1;

        } else {

            new command[200];

            format(command, sizeof(command), "unloadfs %s", fs);

            SendRconCommand(command);

            SendClientMessage(playerid, -1, "{FF00CC}FS descarregado com sucesso.");

        }

    }

    return 1;

}



CMD:carregarfs(playerid, params[]) {

    new fs[128];

    if(Logado[playerid] == true) {

        if(pInfo[playerid][Admin] < 6 || pInfo[playerid][Admin] > 10) {

            return SendClientMessage(playerid, -1, "{C0C0C0}Comando restrito a administradores de nível 6 a 10");

        }

        if(sscanf(params, "s[128]", fs)) {

            SendClientMessage(playerid, -1, "{C0C0C0}Modo de uso: /carregarfs [ nome_fs ]");

            return 1;

        } else {

            new command[200];

            format(command, sizeof(command), "loadfs %s", fs);

            SendRconCommand(command);

            SendClientMessage(playerid, -1, "{FF00CC}FS carregado com sucesso.");

        }

    }

    return 1;

}

CMD:trancarsv(playerid, params[]) {

    new senha[128];

    if(Logado[playerid] == true) {

        if(pInfo[playerid][Admin] < 6 || pInfo[playerid][Admin] > 10) {

            return SendClientMessage(playerid, -1, "{C0C0C0}Comando restrito a administradores de nível 6 a 10");

        }

        if(sscanf(params, "s[128]", senha)) {

            SendClientMessage(playerid, -1, "{C0C0C0}Modo de uso: /trancar [ nova_senha ]");

            return 1;

        } else {

            new command[200];

            format(command, sizeof(command), "password %s", senha);

            SendRconCommand(command);

            SendClientMessage(playerid, -1, "{FF00CC}Senha do servidor alterada com sucesso.");

        }

    }

    return 1;

}

