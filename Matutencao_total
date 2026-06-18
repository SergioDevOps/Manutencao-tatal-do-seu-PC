@echo off
:: Verifica se está rodando como Administrador
net session >nul 2>&1
if %errorLevel% neq 0 (
    echo Por favor, execute este script como ADMINISTRADOR.
    pause
    exit
)

echo ===================================================
echo       INICIANDO MANUTENCAO E OTIMIZACAO TOTAL
echo ===================================================

echo.
echo [1/6] Limpando arquivos temporarios e caches ocultos...
del /q /f /s %TEMP%\*
del /q /f /s C:\Windows\Temp\*
del /q /f /s C:\Windows\Prefetch\*
:: Limpeza do cache de atualizações do Windows (SoftwareDistribution)
net stop wuauserv >nul 2>&1
del /q /f /s C:\Windows\SoftwareDistribution\Download\*
net start wuauserv >nul 2>&1
:: Limpeza do cache da Microsoft Store
wsreset /s
echo Cache e temporarios limpos com sucesso!

echo.
echo [2/6] Limpando e reiniciando a rede (DNS, IP e Sockets)...
ipconfig /flushdns
ipconfig /registerdns
ipconfig /release
ipconfig /renew
netsh winsock reset
netsh int ip reset
echo Rede e DNS redefinidos com sucesso!

echo.
echo [3/6] Verificando integridade dos arquivos do sistema (SFC)...
sfc /scannow

echo.
echo [4/6] Reparando imagem do Windows (DISM)...
dism /online /cleanup-image /restorehealth

echo.
echo [5/6] Otimizando e limpando o armazenamento (Trim/Defrag)...
:: Executa a otimização na unidade C: (Trim para SSD / Defrag para HD)
defrag C: /O

echo.
echo [6/6] Iniciando verificacao rapida de virus (Windows Defender)...
"C:\Program Files\Windows Defender\MpCmdRun.exe" -Scan -ScanType 1

echo.
echo ===================================================
echo   Processo Concluido! Recomenda-se reiniciar o PC.
echo ===================================================
pause
