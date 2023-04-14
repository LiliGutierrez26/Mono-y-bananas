# Mono-y-bananas
Problema del mono y las bananas 

% mueve(Estado1, Movimiento1, Estado2):  El Movimiento1 desde el
% Estado1 conduce al Estado2%   Un estado se representa por un término:
%
%   estado(MonoHorizontal, MonoVertical, PosiciónCaja, TienePlatano)
%
%   con los siguientes valores posibles:
%
%   MonoHorizontal={puerta, debajo, ventana}
%   MonoVertical={suelo, sobre_caja}
%   PosiciónCaja={puerta, debajo, ventana}
%   TienePlátano={tiene, no_tiene}mueve(estado(debajo, sobre_caja, debajo, no_tiene), % Antes de mover
     coge,                                        % Coge el platano
     estado(debajo, sobre_caja, debajo, tiene)). % Tras el movimiento
mueve(estado(P, suelo, P, H),
     sube,                                     % Sube a la caja
     estado(P, sobre_caja, P, H)).
mueve(estado(P1, suelo, P1, H),
     empuja,                                   % Empuja la caja
     estado(P2, suelo, P2, H)).
mueve(estado(P1, suelo, B, H),
     camina,                                  % Camina de P1 a P2
     estado(P2, suelo, B, H)).
% puedecoger(Estado): el mono puede coger el platano en Estado
puedecoger(estado(_, _, _, tiene)).     % 1. El mono ya lo tiene
puedecoger(Estado1):-                   % 2. Hay que trabajar un
                                         %    poco para cogerlo
     mueve(Estado1, Accion, Estado2),   %    Intenta hacer algo
     puedecoger(Estado2).               %    Inténtalo de nuevo
