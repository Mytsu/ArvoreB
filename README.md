# Sistema de Arquivos Formato EXT3

### Definição
O Ext3  é um sistema de arquivos desenvolvido por Stephen C. Tweedie para o UNIX, que tira alguns recursos ao Ext2, dos quais o mais visível é o journaling ou diário. O sistema de arquivos ext3 ou prorrogado terceiro é um sistema de arquivos com diário que é comumente usada pelo kernel Linux. É o padrão do sistema de arquivos para muitos populares distribuições Linux. Stephen C. Tweedie primeiro revelou que ele estava trabalhando na extensão ext2 no Diário do Linux ext2fs Filesystem em um documento de 1998 e mais tarde em uma lista de discussão do destacamento kernel em fevereiro de 1999, e o sistema de arquivos foi fundida com a a linha principal do kernel do Linux em novembro de 2001. Sua principal vantagem sobre ext2 é o diário, que melhora a confiabilidade e elimina a necessidade de verificar o sistema de arquivos após um desligamento abrupto. Seu sucessor é o Ext4.
___

### Funcionamento
#### Journaling 
A principal diferença entre o Ext2 e o Ext3 é a implementação do journaling, que consiste em um registro (log ou journal) de transações cuja finalidade é recuperar o sistema em caso de desligamento não programado.
