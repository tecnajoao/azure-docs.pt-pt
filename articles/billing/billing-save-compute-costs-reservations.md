---
title: O que é o Azure Reservations? | Microsoft Docs
description: Saiba mais sobre as reservas do Azure e preços para guardar nas suas máquinas virtuais, bases de dados SQL, Azure Cosmos DB e outros custos do recurso.
services: billing
author: yashesvi
manager: yashar
ms.service: billing
ms.topic: conceptual
ms.date: 03/22/2019
ms.author: banders
ms.openlocfilehash: 1349a05e1dd235c7b375335ae2c9fed16170a61f
ms.sourcegitcommit: 22ad896b84d2eef878f95963f6dc0910ee098913
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58649396"
---
# <a name="what-are-azure-reservations"></a>O que é o Azure Reservations?

Reservas do Azure ajudam a economizar dinheiro ao pagar previamente para um ano ou três anos de máquinas virtuais, base de dados SQL de computação capacidade, débito do Azure Cosmos DB ou outros recursos do Azure. Pré-pagamento permite-lhe obter um desconto sobre os recursos que utiliza. As reservas podem reduzir significativamente a sua máquina virtual, a computação de base de dados SQL, Azure Cosmos DB, ou outros recursos de custos até 72% em preços pay as you go. Reservas de fornecem um desconto de faturação e não afetam o estado de tempo de execução dos seus recursos.

Pode comprar uma reserva [portal do Azure](https://aka.ms/reservations). Para obter mais informações, veja os artigos seguintes:

Planos de serviço:
- [Máquinas virtuais com instâncias de VM reservadas do Azure](../virtual-machines/windows/prepay-reserved-vm-instances.md)
- [Capacidade de reserva de recursos do Azure do Cosmos DB com o Azure Cosmos DB](../cosmos-db/cosmos-db-reserved-capacity.md)
- [Capacidade de reserva de recursos de computação de base de dados SQL com a base de dados do Azure SQL](../sql-database/sql-database-reserved-capacity.md)

Planos de software:
- [Planos de software do Red Hat do Azure reservas](../virtual-machines/linux/prepay-rhel-software-charges.md)
- [Planos de software SUSE das reservas do Azure](../virtual-machines/linux/prepay-suse-software-charges.md)

## <a name="why-buy-a-reservation"></a>Por que devo adquirir uma reserva?

Se tiver máquinas virtuais, Azure Cosmos DB ou bases de dados do SQL que são executadas durante longos períodos de tempo, ter de comprar uma reserva dá-lhe a opção mais económica. Por exemplo, quando executar quatro instâncias de um serviço sem uma reserva continuamente, lhe é cobrada às tarifas pay as you go. Se comprar uma reserva para esses recursos, obtém imediatamente o desconto de reserva. Os recursos já não são cobrados às tarifas pay as you go.

## <a name="charges-covered-by-reservation"></a>Custos abrangidos por reserva

Planos de serviço:

- Instância de Máquina Virtual reservada: Uma reserva abrange apenas os custos de computação de máquina virtual. Não cobre custos adicionais de software, sistema de rede ou armazenamento.
- O Azure Cosmos DB a capacidade de reserva: Uma reserva abrange o débito aprovisionado para os seus recursos. Não abrange a armazenamento e os encargos de rede.
- Base de dados SQL reservados vCore: Apenas os custos de computação são incluídos com uma reserva. A licença é faturada em separado.
- O Azure Cosmos DB a capacidade de reserva: Uma reserva abrange o débito aprovisionado para os seus recursos, apesar de não abranger os custos de armazenamento e rede.

Para as máquinas virtuais do Windows e a base de dados SQL, que podem ser cobertos os custos de licenciamento com [benefício híbrido do Azure](https://azure.microsoft.com/pricing/hybrid-benefit/).

## <a name="whos-eligible-to-purchase-a-reservation"></a>Quem é elegível para comprar uma reserva?

Para comprar um plano, tem de ter uma função de proprietário da subscrição de uma empresa (MS-AZR - 0017P ou MS-AZR - 0148P) ou uma subscrição pay as you go (MS-AZR - 003P ou MS-AZR - 0023P). Fornecedores de soluções cloud, podem utilizar o portal do Azure ou [Centro de parceiros](/partner-center/azure-reservations) comprar reservas do Azure.

Clientes com contrato EA podem limitar as compras aos administradores EA, desativando a **adicionar as instâncias reservadas** opção no Portal de EA. Os administradores EA tem de ser um proprietário da subscrição pelo menos uma subscrição de EA para comprar uma reserva. A opção é útil para as empresas que querem uma equipe centralizada para comprar reservas para centros de custos diferentes. Após a compra, as equipes centralizadas podem adicionar os proprietários do Centro de custos para as reservas. Os proprietários podem, em seguida, definir o âmbito da reserva para suas assinaturas. A equipe central não precisa ter acesso de proprietário da subscrição em que a reserva é comprada.

Um desconto de reserva aplica-se apenas aos recursos associados a tipos de subscrição Enterprise, pay as you go ou CSP.

## <a name="how-is-a-reservation-billed"></a>Como é faturada uma reserva?

A reserva é cobrada ao método de pagamento associado à subscrição. Se tiver uma subscrição Enterprise, o custo da reserva é deduzido da seu saldo de alocação monetária. Se o seu saldo de alocação monetária não abrange o custo da reserva, é-lhe cobrada a utilização excedida. Se tiver uma subscrição pay as you go, o cartão de crédito que tem na sua conta é cobrado imediatamente. Se a faturação por fatura, verá os custos na sua fatura seguinte.

## <a name="how-reservation-discount-is-applied"></a>Como o desconto de reserva é aplicado

O desconto de reserva se aplica a utilização de recursos que corresponda os atributos que selecionou quando comprar a reserva. Os atributos incluem o âmbito em que executar as VMs correspondentes, bases de dados SQL, Azure Cosmos DB ou outros recursos. Por exemplo, se pretender que um desconto de reserva para quatro máquinas de virtuais de Standard D2 na região E.U.A. oeste, selecione a subscrição em que as VMs estão em execução. Se as máquinas virtuais são executadas em subscrições diferentes na sua conta/inscrição, em seguida, selecione o âmbito como partilhado. Âmbito partilhado permite que o desconto de reserva a ser aplicado entre subscrições. Pode alterar o âmbito depois de comprar uma reserva. Para obter mais informações, consulte [Gerir reservas de Azure](billing-manage-reserved-vm-instance.md).

Um desconto de reserva aplica-se apenas aos recursos associados a tipos de subscrição Enterprise, pay as you go ou CSP. Recursos que são executados numa subscrição com outros tipos de oferta não recebem o desconto de reserva.

Para compreender melhor como as reservas afeta sua faturação, veja os artigos seguintes:

Planos de serviço:

- [Compreender o que desconto de instâncias de VM reservadas do Azure](billing-understand-vm-reservation-charges.md)
- [Compreender o desconto de reserva do Azure](billing-understand-vm-reservation-charges.md)
- [Compreender o desconto de reserva do Azure Cosmos DB](billing-understand-cosmosdb-reservation-charges.md)

Planos de software:

- [Compreender o desconto de reserva do Azure e a utilização do Red Hat](billing-understand-rhel-reservation-charges.md)
- [Compreender o desconto de reserva do Azure e a utilização do SUSE](billing-understand-suse-reservation-charges.md)

## <a name="when-the-reservation-term-expires"></a>Quando expira o termo de reserva

No final do período de reserva, expira o desconto de faturação e a máquina virtual, base de dados SQL, Azure Cosmos DB ou outro recurso é cobrada de acordo com o pay as you acedo preço. Reservas do Azure não a renovação automática. Para continuar a obter o desconto de faturação, tem de comprar uma reserva nova para o software e serviços elegíveis.

## <a name="discount-applies-to-different-sizes"></a>Desconto aplica-se a tamanhos diferentes

Ao comprar uma reserva, pode aplicar o desconto para as outras instâncias com atributos que estão dentro do mesmo grupo de tamanho. Esta funcionalidade é conhecida como a flexibilidade de tamanho de instância. A flexibilidade da cobertura de desconto depende do tipo de reserva e os atributos que escolher quando comprar a reserva.

Planos de serviço:

- Instâncias reservadas da VM: Quando comprar a reserva e selecionar **otimizado para**: **flexibilidade de tamanho de instância**, a cobertura de desconto depende de selecionar o tamanho da VM. A reserva pode aplicar os tamanhos de máquinas virtuais (VMs) no mesmo grupo de séries de tamanho. Para obter mais informações, consulte [flexibilidade de tamanho de Máquina Virtual com as instâncias de VM reservadas](../virtual-machines/windows/reserved-vm-instance-size-flexibility.md).
- Capacidade de reserva de base de dados SQL: A cobertura de desconto depende do escalão de desempenho que escolher. Para obter mais informações, consulte [compreender a forma como um desconto de reserva do Azure é aplicado](billing-understand-reservation-charges.md).
- O Azure Cosmos DB a capacidade de reserva: A cobertura de desconto depende do débito aprovisionado. Para obter mais informações, consulte [compreender como é aplicado um desconto de reserva do Azure Cosmos DB](billing-understand-cosmosdb-reservation-charges.md).

## <a name="need-help-contact-us"></a>Precisa de ajuda? Contacte-nos.

Se tiver alguma dúvida ou precisar de ajuda, [criar um pedido de suporte](https://go.microsoft.com/fwlink/?linkid=2083458).

## <a name="next-steps"></a>Passos Seguintes

- Iniciar a guardar nas suas máquinas virtuais ao comprar uma [instância de VM reservada](../virtual-machines/windows/prepay-reserved-vm-instances.md), [capacidade de reserva de base de dados SQL](../sql-database/sql-database-reserved-capacity.md), ou [capacidade de reserva do Azure Cosmos DB](../cosmos-db/cosmos-db-reserved-capacity.md).
- Saiba mais sobre as reservas do Azure com os seguintes artigos:
    - [Gerir o Azure Reservations](billing-manage-reserved-vm-instance.md)
    - [Compreender a utilização de reserva para a sua subscrição pay as you go](billing-understand-reserved-instance-usage.md)
    - [Compreender a utilização de reserva para inscrição da sua empresa](billing-understand-reserved-instance-usage-ea.md)
    - [Custos de software do Windows não incluídos com reservas](billing-reserved-instance-windows-software-costs.md)
    - [Reservas do Azure no programa de fornecedor de soluções (CSP) do parceiro Center na nuvem](https://docs.microsoft.com/partner-center/azure-reservations)
