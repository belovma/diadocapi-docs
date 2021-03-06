GenerateAcceptanceCertificateXmlForBuyer
========================================

Имя ресурса: **/GenerateAcceptanceCertificateXmlForBuyer**

HTTP метод: **POST**

Параметры строки запроса:

-  *boxId*: идентификатор ящика;

-  *sellerTitleMessageId*: идентификатор сообщения, содержащего соответствующий титул исполнителя;

-  *sellerTitleAttachmentId*: идентификатор сущности, представляющей титул исполнителя, для которого требуется изготовить титул заказчика;

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../Authorization>`.

В теле запроса должны содержаться данные для изготовления титула заказчика для акта о выполнении работ / оказании услуг в XML-формате, в виде сериализованной структуры :doc:`AcceptanceCertificateBuyerTitleInfo <../proto/AcceptanceCertificateInfo>`.

В теле ответа содержится XML-файл титула заказчика для акта о выполнении работ / оказании услуг, построенный на основании данных из запроса. 

Файл изготавливается в соответствии с :download:`XML-схемой <../xsd/DP_ZAKTPRM_1_990_00_05_01_02.xsd>`, которая описывает рекомендованный ФНС формат для электронных актов о выполнении работ / оказании услуг. Имя файла титула заказчика для акта возвращается в стандартном HTTP-заголовке Content-Disposition.

Для вызова этого метода текущий пользователь должен иметь доступ к документу титула продавца, в противном случае возвращается код ошибки 403 (Forbidden).

Возможные HTTP-коды возврата:

-  200 (OK) - операция успешно завершена;

-  400 (Bad Request) - данные в запросе имеют неверный формат или отсутствуют обязательные параметры;

-  401 (Unauthorized) - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные;

-  403 (Forbidden) - доступ к ящику с предоставленным авторизационным токеном запрещен;

-  404 (Not Found) - в указанном ящике нет сообщения с идентификатором sellerTitleMessageId, либо в указанном сообщении нет сущности с идентификатором sellerTitleAttachmentId;

-  405 (Method not allowed) - используется неподходящий HTTP-метод;

-  409 (Conflict) - не удалось разобрать соответствующий титул исполнителя;

-  500 (Internal server error) - при обработке запроса возникла непредвиденная ошибка;