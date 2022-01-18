FROM plutarch_ppp-nix:latest

ARG user=ppp
USER $user
WORKDIR /home/$user

RUN mkdir -p ~/.config/nix
RUN echo 'substituters = https://hydra.iohk.io https://iohk.cachix.org https://cache.nixos.org/' >> ~/.config/nix/nix.conf
RUN echo 'trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= iohk.cachix.org-1:DpRUyj7h7V830dp/i6Nti+NEO2/nhblbov/8MW7Rqoo= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=' >> ~/.config/nix/nix.conf

# Install other useful tools

# RUN sudo apt-get install -y less

ENV USER=ppp
RUN bash --login -c "nix-env --version"
COPY plutus.sh /home/ppp/plutus.sh

RUN bash --login plutus.sh

# this doesn't work - you get:
# error: experimental Nix feature 'nix-command' is disabled; use '--extra-experimental-features nix-command' to override
# RUN bash --login -c "nix build -f default.nix plutus.haskell.packages.plutus-core"

RUN bash --login -c "cd plutus && nix --extra-experimental-features nix-command build -f default.nix plutus.haskell.packages.plutus-core"
RUN bash --login -c "cd plutus && nix-shell"