#*****************************************************************
# File:   Makefile_p5_e1
# Author: PSCD-Unizar
# Date:   octubre 2018
# Coms:   Ejemplo de Makefile para la práctica 5 de PSCD
#         "make -f Makefile_p5_e1" construye todos los ejecutables
#         "make -f Makefile_p5_e1 Cliente" construye "Cliente"
#         ....
#         Es necesario descomentar la línea 28 para poder compilar en hendrix
#*****************************************************************

#---------------------------------------------------------
CC=g++

DRIVER=LindaDriver
MONITOR=monitorLinda
#Clientes
CLIENT=mainLindaDriver
OCLIENT=clienteInteractivo
MIXTO=clienteMixto
TEST=test
BRUTA=bruta
#Fin de clientes
SERVER=servidorLinda
TUPLAS=tuplas
SERVEI=servei
SOCKET_DIR=Socket
SOCKET=${SOCKET_DIR}/Socket

CPPFLAGS=-I. -I${SOCKET_DIR} -O2 -std=c++11 -lsockets -Wall# Flags compilacion
LDFLAGS=-pthread # Flags linkado threads

all: ${CLIENT} ${SERVER} ${SERVEI} ${OCLIENT} ${TEST} ${BRUTA} ${MIXTO}
#----------------------------------------------------------------------------
#Para gestionar opciones de compilación según la máquina: hendrix tiene sus manías
#Descomentar la siguiente línea para compilar en hendrix
#SOCKETSFLAGS=-lsocket -lnsl
#-----------------------------------------------------------
# MONITOR
# Compilacion
${MONITOR}.o: ${MONITOR}.hpp ${MONITOR}.cpp
	${CC} -c ${CPPFLAGS} ${MONITOR}.cpp

# Linkado
${MONITOR}: ${TUPLAS}.o ${SOCKET}.o ${MONITOR}.o  
	${CC} ${TUPLAS}.o ${SOCKET}.o ${MONITOR}.o -o ${MONITOR} ${SOCKETSFLAGS}
#-----------------------------------------------------------
# DRIVER
# Compilacion
${DRIVER}.o: ${DRIVER}.hpp ${DRIVER}.cpp
	${CC} -c ${CPPFLAGS} ${DRIVER}.cpp

# Linkado
${DRIVER}: ${TUPLAS}.o ${SOCKET}.o ${DRIVER}.o  
	${CC} ${LDFLAGS} ${TUPLAS}.o ${SOCKET}.o ${DRIVER}.o -o ${DRIVER} ${SOCKETSFLAGS}
#-----------------------------------------------------------
# CLIENTE
# Compilacion
${CLIENT}.o: ${CLIENT}.cpp
	${CC} -c ${CPPFLAGS} ${CLIENT}.cpp

# Linkado
${CLIENT}: ${DRIVER}.o ${TUPLAS}.o ${SOCKET}.o ${CLIENT}.o  
	${CC} ${LDFLAGS} ${DRIVER}.o ${TUPLAS}.o ${SOCKET}.o ${CLIENT}.o -o ${CLIENT} ${SOCKETSFLAGS}
#-----------------------------------------------------------
# MIXTO
# Compilacion
${MIXTO}.o: ${MIXTO}.cpp
	${CC} -c ${CPPFLAGS} ${MIXTO}.cpp

# Linkado
${MIXTO}: ${DRIVER}.o ${TUPLAS}.o ${SOCKET}.o ${MIXTO}.o  
	${CC} ${LDFLAGS} ${DRIVER}.o ${TUPLAS}.o ${SOCKET}.o ${MIXTO}.o -o ${MIXTO} ${SOCKETSFLAGS}
#-----------------------------------------------------------
# BRUTA
# Compilacion
${BRUTA}.o: ${BRUTA}.cpp
	${CC} -c ${CPPFLAGS} ${BRUTA}.cpp

# Linkado
${BRUTA}: ${DRIVER}.o ${TUPLAS}.o ${SOCKET}.o ${BRUTA}.o  
	${CC} ${LDFLAGS} ${DRIVER}.o ${TUPLAS}.o ${SOCKET}.o ${BRUTA}.o -o ${BRUTA} ${SOCKETSFLAGS}
#-----------------------------------------------------------
# TESTEO
# Compilacion
${TEST}.o: ${TEST}.cpp
	${CC} -c ${CPPFLAGS} ${TEST}.cpp

# Linkado
${TEST}: ${DRIVER}.o ${TUPLAS}.o ${SOCKET}.o ${TEST}.o  
	${CC} ${LDFLAGS} ${DRIVER}.o ${TUPLAS}.o ${SOCKET}.o ${TEST}.o -o ${TEST} ${SOCKETSFLAGS}
#-----------------------------------------------------------
# OTROCLIENTE
# Compilacion
${OCLIENT}.o: ${OCLIENT}.cpp
	${CC} -c ${CPPFLAGS} ${OCLIENT}.cpp

# Linkado
${OCLIENT}: ${DRIVER}.o ${TUPLAS}.o ${SOCKET}.o ${OCLIENT}.o  
	${CC} ${LDFLAGS} ${DRIVER}.o ${TUPLAS}.o ${SOCKET}.o ${OCLIENT}.o -o ${OCLIENT} ${SOCKETSFLAGS}
#-----------------------------------------------------------
# SERVIDOR
# Compilacion
${SERVER}.o: ${SERVER}.cpp 
	${CC} -c ${CPPFLAGS} ${SERVER}.cpp

# Linkado
${SERVER}: ${TUPLAS}.o ${SOCKET}.o ${SERVER}.o
	${CC} ${LDFLAGS} ${TUPLAS}.o ${SOCKET}.o ${SERVER}.o -o ${SERVER} ${SOCKETSFLAGS}
#-----------------------------------------------------------
# SERVEI
# Compilacion
${SERVEI}.o: ${SERVEI}.cpp 
	${CC} -c ${CPPFLAGS} ${SERVEI}.cpp

# Linkado
${SERVEI}: ${TUPLAS}.o ${MONITOR}.o ${SOCKET}.o ${SERVEI}.o
	${CC} ${LDFLAGS} ${TUPLAS}.o ${MONITOR}.o ${SOCKET}.o ${SERVEI}.o -o ${SERVEI} ${SOCKETSFLAGS}
#-----------------------------------------------------------
# SOCKETS
# Compilacion libreria de Sockets
${SOCKET}.o: ${SOCKET}.hpp ${SOCKET}.cpp
	${CC} -c ${CPPFLAGS} ${SOCKET}.cpp -o ${SOCKET}.o
#-----------------------------------------------------------
# TUPLAS
# Compilacion
${TUPLAS}.o: ${TUPLAS}.hpp  ${TUPLAS}.cpp 
	${CC} -c ${CPPFLAGS} ${TUPLAS}.cpp -o ${TUPLAS}.o
#-----------------------------------------------------------		
# LIMPIEZA
clean:
	$(RM) ${SOCKET}.o
	$(RM) ${TUPLAS}.o
	$(RM) ${CLIENT} ${CLIENT}.o
	$(RM) ${BRUTA} ${BRUTA}.o
	$(RM) ${TEST} ${TEST}.o
	$(RM) ${MIXTO} ${MIXTO}.o
	$(RM) ${OCLIENT} ${OCLIENT}.o
	$(RM) ${SERVER} ${SERVER}.o
	$(RM) ${SERVEI} ${SERVEI}.o
	$(RM) ${DRIVER} ${DRIVER}.o
	$(RM) ${MONITOR} ${MONITOR}.o
