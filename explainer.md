> 中文翻译：曾毅 (https://github.com/studyzy/)

# 可验证凭证（Verifiable Credentials）数据模型说明

***作者：Tzviya Siegman, Wiley; Manu Sporny, Digital Bazaar; Ken Ebert, Sovrin;
Brent Zundel, Evernym***

***注意***："可验证声明（Verifiable Claims）"现在被称为"可验证凭证（Verifiable Credentials）"。
W3C Verifiable Claims Working Group 在使用"可验证声明"一词时发现该术语容易导致混淆。
该工作组此后已达成共识，转而使用"可验证凭证"一词，其中包含"声明（claims）"。

## 介绍

目前，在互联网上传输驾驶执照、年龄证明、教育资质和医疗数据等凭证，
并以可验证且保护个人隐私的方式进行，仍然十分困难。

从 2013 年开始，
[W3C Credentials Community Group](https://w3c-ccg.github.io/) 开始认真着手该领域的解决方案，随后
[Rebooting Web of Trust Community](http://www.weboftrust.info/) 和
[Verifiable Claims Working Group](https://www.w3.org/2017/vc/) 也相继加入。这些由 150 多位个人和组织组成的工作组，目前专注于数字凭证的创建、存储、传输和验证。

## 目标

Verifiable Claims Working Group (VCWG) 的使命是使声明的表达、交换和验证更加简单和安全。该数据模型概述了核心概念，如声明、凭证和展示，这些构成了规范的基础。

## 非目标

VCWG 不定义协议或 API。该模型与标识符无关。

## 入门

可验证凭证生态系统由五个主要角色组成：

* ***颁发者（issuer）*** - 实体可能执行的一种角色，通过创建可验证凭证，将其与特定***主体（subject）***关联，并将其传输给***持有者（holder）***。颁发者的示例包括公司、非营利组织、行业协会、政府和个人。

* ***主体*** - 实体可能执行的一种角色，拥有一个或多个关于它的可验证凭证声明。主体的示例包括人类、动物和物品。
  
* ***持有者*** - 实体可能执行的一种角色，拥有关于某个主体的一个或多个可验证凭证，并从中生成展示。持有者的示例包括学生、员工和客户。
  
* ***验证者（verifier）*** - 实体可能执行的一种角色，通过请求和接收可验证展示（verifiable presentation）来证明持有者拥有所需的可验证凭证。验证者的示例包括雇主、安全人员和网站。

* ***可验证数据注册表（verifiable data registry）*** - 系统可能执行的一种角色，通过协调标识符、密钥和其他相关数据（如可验证凭证模式和撤销注册表）的创建和验证，这些可能是使用可验证凭证所必需的。某些配置可能需要主体的可关联标识符。可验证数据注册表的示例包括受信任的数据库、去中心化数据库、政府身份证数据库和分布式账本。

**注意：** 在许多情况下，可验证凭证的持有者和主体是同一个人，但并非总是如此。例如，父母（持有者）可能持有孩子（主体）的可验证凭证，或者宠物爱好者（持有者）可能持有其宠物（主体）的可验证凭证。

可验证凭证生态系统的可视化描述如下所示。

<a href="https://w3c.github.io/vc-data-model/">
  <img src="diagrams/ecosystem.svg" width="100%" height="400">
</a>

### 声明、凭证和展示

生态系统角色交换数据以实现下面概述的用例。交换的数据因参与的角色不同而异，但基本上由声明、凭证和展示组成。

*声明*是关于主体的陈述，表达为主体-属性-值的关系。

<a href="https://w3c.github.io/vc-data-model/">
  <img src="diagrams/claim.svg" width="50%">
</a>

### 证明（Proofs）

用于证明可验证凭证或可验证展示中的信息未被篡改的加密机制被称为*证明（proof）*。有许多类型的加密证明，包括但不限于数字签名、零知识证明（zero-knowledge proof）、工作量证明和权益证明。

数据模型不详细说明证明机制。

#### 零知识证明

可验证凭证数据模型支持使用零知识证明 (ZKP) 技术。这允许具有 ZKP 兼容元素的凭证支持以下展示功能：

* 每个凭证属性的选择性披露（selective disclosure）。
* 数值（例如整数、日期和枚举）的谓词证明：
  * 大于
  * 小于
  * 在某个范围内（例如，5 < x < 100）。
* 集合成员资格证明。

## 用例

VCWG 已创建了一份[用例](https://w3c.github.io/vc-use-cases/)文档，展示了复杂场景和完整编码。

一些简单的用例包括：
* 一名学生出示政府颁发的身份证明，以在参加标准化考试时验证其身份。
* 一家航空公司使用数字优惠券为忠实客户提供头等舱升级。这些优惠券以可验证凭证的形式颁发。
* 一个医师委员会在凭证存储库（credential repository）中维护其经过认证的医师名单，使委员会能够断言医师已获得认证，或根据需要撤销认证。当医师申请职位时，或患者寻找其正在考虑的医生的信息时，可以验证存储库中的信息。这可以通过集合成员资格的零知识证明来完成。
* 一位贷款申请者提供足够收入的证明，该证明来源于其雇主颁发的凭证。这可以通过零知识谓词证明来完成，而无需透露其确切收入。

## 代码示例

可验证凭证是什么样的？

可验证凭证中 MAY 包含许多信息，规范中有大量示例。

以下是凭证中 ID 属性的示例，使用了去中心化标识符 (DID) 方案。

```
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://example.com/examples/v1"
  ],
  "id": "http://example.edu/credentials/1872",
  "type": ["VerifiableCredential", "AlumniCredential"],
  "issuer": "https://example.edu/issuers/565049",,
  "issuanceDate": "2010-01-01T19:73:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "alumniOf": "Example University"
  },
  "proof": {
    "type": "RsaSignature2018",
    "created": "2017-06-18T21:19:10Z",
    "verificationMethod": "https://example.com/jdoe/keys/1",
    "jws": "BavEll0/I1zpYw8XNi1bgVg/sCneO4Jugez8RwDg/+
      MCRVpjOboDoe4SxxKjkCOvKiCHGDvc4krqi6Z1n0UfqzxGfmatCuFibcC1wps
      PRdW+gGsutPTLzvueMWmFhwYmfIFpbBu95t501+rSLHIEuujM/+PXr9Cky6Ed
      +W3JT24="
  }
}
```

以下是支持 ZKP 的可验证凭证示例。
```
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "ctx:sov:anoncred:v1",
    "ctx:sov:GppHbMLLeKNYRhcQiXh3GjP2Yh",
  ],
  "type": [
    "VerifiableCredential",
    "AnonCred",
    "ExampleNameDOB"
  ],
  "issuer": "did:sov:4t1FPo72LzDMwpqtTVGVjysD6GUqS",
  "issuanceDate": "2018-11-27T12:37:15Z",
  "credentialSubject": {
    "name": "John Doe",
    "birthDate": "1969-02-14",
  },
  "proof": {
    "m_2": "0x375A05242CF33E9AE2E527DB6D6D5A2FA78A3042EF25D21013F82D5C642E98FA",
    "attributes": [
      "0x6998340478030A68F6DB6A3D4CB94304C4C60576E0992CBE81C4D32764876AD4",
      "0x5BFD3A7B",
      "0x3C414697B170EB2691A2AE126DD07F936005C478FFAEDB3B67255DA017C64A4B",
      "0x629E",
    ],
    "cred_def": "cdf:sov:Q6kuSqnxE57waPFs2xAs7q:3:CL:12:CDL1",
    "signature": {
      "A": "0x2B048AFC2099E78A4F11C75FE913ECDAFDE07911D1D54F439ECC5CDB1AC952E95309DB6D809F31E1A0C2326E3603A21DD7F29E11AA2ABA9D5B077A53EF49C45EF9FA757508708B5FBE26EB4D21CC63C40BDC785E758A106FFB9654D8E8B9B1A34A7DA26E8BF6174DF6C735D909EE32B44200E36616C31EA6DDBFC252004F68A30BEE16A714C75DB60D920DB3E6B18622C6944C75337FB1CB8E3AC928CB182ABE49AD76EBE19063D1353D159341DEB76B9D6732A77B45BC5EBD35A6B7AC4C39CCDCDF846281B130D5A5E22CA6F8479F8CDBE3293E317AE4EC5A0716EE1B6348B6D6C196FCE1A594F57FF8999E57AAC8EC54C99296E9D35EE3FEDFB20ACBE97533C"
      "e": "0x1000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000006887BBE4F8F22F6FF0EE2863E42615"
      "v": "0x8639169982733C9D95BC8782C3566E1774BAAFA4B048648BFEF3ACB588A0488982E123B69B09FD03DF501824895FD670F77CB6B832F97FAA85F746B0869EAFB4A358214103B4AB00A4993A1AD9EB1DE0A980818D7C6C085112713989444EEC04D07E99D5C827A76DA4E24BC2F445CB82658F6A079AB03C002E8812C79E1E155CFAEAA12046BAD5C51DE2292DEA64AFB61387813DEC96B2485E84D2039E571ACAF3BA9A820918EE9616300D8D970C1211C7F71966C008FC56D0D8136A1B43074C2AAF3C39E4E59ED4A5C3EB355352083497332B1B37C591DC7786C4A000C6D087C9C7C039CFCB137EAE7B905D5881E94AC626F1B0945D7FDC74CDFADE02D67449706146FE43A32AF560E84CCA7A0FF351F5FD266C3D7D0C1EB1A056BC257392CE170D25CC24918FDA1DBFE4F9BEE702410276C115BE3E0680445429DFAA2B07F2C51296DD3508C796B90A7EB1D301E8079D6CC8099"
    },
    "signature_correctness_proof": {
      "se": "0x2CEF1A529FC0C64EC2D14BF7555E726F99061CBD6C41365401203FE81139496EDB4763FDEFF85124C8CC8DA0C60E16E3B68E57B9A1014B2CA99656AAF69BF7C1B1FA298C16FC6A7FB16E009B5CF03568113BCACBDAF927E04808F5032476274B4302EBDA632B721A3C0899B82762AC436564770E5B34EE85AEEDA43E87A1BBB82FCB2BAA179EA1FE9046CE43FCB5FF589650578518867E40DA438C5DA01B2CB7166650B7546F451A11652EBB80A3FA7193092233533A42BFA19897D6C17964E19826E0F50FA81CEFDB91DC954DFCFE0029463A224CA8DE2AA6A16D64EBCE4208350130E3CC560048863B424CBD9D6FADD780B40B4DD8D3BC1501B2E5FBFCBA8C",
      "c": "0xD074B91DC755D75F56BA00F0B650190CF7035BFBE65678A290A511DFEF554521"
    }
  }
}
```

以下是编码为 JWT 并支持 JWS 证明的可验证凭证示例。该示例展示了头部和有效载荷，以及最终的 JWS 紧凑序列化（base64 编码）。
```
{
    "alg": "RS256",
    "typ": "JWT",
    "kid": "did:example:abfe13f712120431c276e12ecab#keys-1"
}

{
  "sub": "did:example:ebfeb1f712ebc6f1c276e12ec21",
  "jti": "http://example.edu/credentials/3732",
  "iss": "did:example:abfe13f712120431c276e12ecab",
  "iat": "1541493724",
  "exp": "1573029723",
  "nonce": "660!6345FSer",
  "vc": {
    "@context": [
      "https://www.w3.org/2018/credentials/v1",
      "https://example.com/examples/v1"
    ],
    "type": ["VerifiableCredential", "UniversityDegreeCredential"],
    "credentialSubject": {
      "degree": {
        "type": "BachelorDegree",
        "name": "Bachelor of Science in Mechanical Engineering"
      }
    }
  }
}

eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6ImRpZDpleGFtcGxlOmFiZmUxM2Y3MTIxMjA0
MzFjMjc2ZTEyZWNhYiNrZXlzLTEifQ.eyJzdWIiOiJkaWQ6ZXhhbXBsZTplYmZlYjFmNzEyZWJjNmYxY
zI3NmUxMmVjMjEiLCJqdGkiOiJodHRwOi8vZXhhbXBsZS5lZHUvY3JlZGVudGlhbHMvMzczMiIsImlzc
yI6ImRpZDpleGFtcGxlOmFiZmUxM2Y3MTIxMjA0MzFjMjc2ZTEyZWNhYiIsImlhdCI6IjE1NDE0OTM3M
jQiLCJleHAiOiIxNTczMDI5NzIzIiwibm9uY2UiOiI2NjAhNjM0NUZTZXIiLCJ2YyI6eyJAY29udGV4d
CI6WyJodHRwczovL3czLm9yZy8yMDE4L2NyZWRlbnRpYWxzL3YxIiwiaHR0cHM6Ly9leGFtcGxlLmNvb
S9leGFtcGxlcy92MSJdLCJ0eXBlIjpbIlZlcmlmaWFibGVDcmVkZW50aWFsIiwiVW5pdmVyc2l0eURlZ
3JlZUNyZWRlbnRpYWwiXSwiY3JlZGVudGlhbFN1YmplY3QiOnsiZGVncmVlIjp7InR5cGUiOiJCYWNoZ
WxvckRlZ3JlZSIsIm5hbWUiOiJCYWNoZWxvciBvZiBTY2llbmNlIGluIE1lY2hhbmljYWwgRW5naW5lZ
XJpbmcifX19fQ.VTotLRYblDOtJBTlOYbvibqC_uu8RXdvv6m_lR6cdEdFcGf4oNKiFZ_WJr07n1A-_E
jTLzjD5XwmDPzb8lxDlEkCLJ5WQS4_jwzCZAeetNG7YO2slTCFRiE_2xBM2R01ssI8bEPnqLBnc-Lu88
DmO21wL8-Yud1eL45N_pEE5DqTF5DJ-IesmVkWvC8159GUHKShFIpgHiE1EDDEjUzjYA5ZyzS2_ZmSTj
5NDLOt8muVlORpO7xJ6aWRdtibkmSTKykUzh75-4Rklz2H9-AWBXEh5ajkyB8yINh_y4jK3g7ypVACRI
Z9DZhdw2K39KCilAPVJsmejiKlxNhQAOlgcYUlhCzphLsqo-FA90fFGrsg-3JuQihnNw6RSPImjVt_yV
appfjilEzhyfWT-Smm_KN8LRbFdNtU-awwhKbjDNW-7fNVrnsWHKvLsd_zlch8YlHZ6g0tHJnxo_yOTM
BSSpt0jzyl1ByqjumgBFNpTR-NTVog4B7vLEvq58RuShraL5VNr7bjNzq2gisp3jq3LpfUmiwc7rQXw6
AlQuattLRolXx3EtPysrZe-wU7yrEtNPvpGs-OyJAczfJPzza9lGTbx6IWS-0pTmNq6hwNd0ODMiB3uL
3TeBN1xLoue9Hdc3toUvmdyXecSvltPcaiRoN-uQo8RRAvfK7GALAzaHw
```

## 重要的设计选择

本节总结了 VCWG 花费大量时间讨论的若干设计选择。

### 隐私增强架构的灵活性

VCWG 花费了大量时间探索各种隐私问题，包括但不限于多种 ZKP 系统、选择性披露方案、避免加密指纹识别，以及跟踪技术与可验证凭证的交叉问题。其结果是一个试图在当前可实现的目标与确保未来隐私增强系统能够使用相同架构来保护个人和组织隐私之间取得适当平衡的规范。

### 语法灵活性

虽然该文档概述了一个可以用多种不同语法表达的数据模型，但在规范应突出哪些表示语法的问题上经过了深思熟虑。JSON-LD 作为 JSON 的完全兼容子集，被建议作为主要格式。曾有人担心处理可验证凭证需要 JSON-LD 处理器。经过一年多的技术工作以及与 JSON-LD 1.1 Working Group 的合作，VCWG 已经证明符合规范并不需要 JSON-LD 处理器。绝大多数开发者将能够像处理普通 JSON 对象一样处理可验证凭证。

### 授权

VCWG 讨论了将可验证凭证用作授权机制的问题。讨论的结果是：可验证凭证可以在授权系统中使用，但其本身并不构成授权系统，并且任何在授权框架中使用可验证凭证的系统都应该进行充分考虑。

### 使用条款

关于可验证凭证应如何使用，进行了多次讨论。例如，颁发者可能希望对可验证凭证的使用方式施加限制。持有者可能也希望对验证者如何使用其信息施加限制。虽然对于这些限制应该能够在数据模型中表达已达成共识，但对于规范应建议哪些类型的限制则没有达成共识。结果是一个用于表达可验证凭证和可验证展示使用条款的开放机制。

### 证明格式灵活性

目前，VCWG 参与者至少有四种不同的证明格式在积极使用中，包括 JSON Web Signatures、使用 CL 签名的零知识证明、Common Binary Object Representation Object Signing and Encryption，以及 Linked Data Proofs。VCWG 很难选择一种格式，因为每种方法都有各自的优缺点。为了应对这一挑战，VCWG 确保了可验证凭证数据模型足够灵活，能够与每种签名格式兼容，而无需对核心数据模型进行任何更改。

### 对 JWT 的支持

JSON Web Token (JWT) 是一种广泛使用的在两方之间表达声明的方式。为 JWT 提供可验证凭证数据模型的表示，使现有系统和库能够参与该生态系统。

规范定义了可验证凭证数据模型到 JWT 和 JWS 的编码规则。它还定义了关于何时以及如何使用特定 JWT 注册声明名称和特定 JWS 注册头部参数名称的处理规则，使基于 JWT 的系统能够符合规范，同时避免在封闭的 JSON 或 JSON-LD 对象中重复表示特定信息。

### 选择性披露
持有者选择性披露凭证中属性的能力被认为是一个有价值的特性，与数据最小化和自主身份的原则相一致。

曾讨论过是否应该要求所有可验证凭证实现者都具备此特性，但最终确定要求此类能力可能过于繁重。当前形式的数据模型支持选择性披露作为最佳实践，但不要求必须实现。

## 有风险的功能

我们已向[潜在实现者征求了初步承诺](https://docs.google.com/spreadsheets/d/1SzfAUA0J72-1BORHJEmY4cdZrQ6vmKy4oq_24r_NwB4/edit?usp=sharing)。我们期望所有功能至少有两个实现。根据目前的承诺，某些功能恰好只有两个实现。当然，我们将继续招募更多的实现。

## 实现和审查

VCWG 已开始横向审查流程。来自 APA 和 PING 的反馈已经被纳入或正在纳入过程中。

该数据模型已有众多成功的实现，包括政府、大学、主要技术组织和非营利组织。

## 参考资料和致谢

大部分文本来自[数据模型](https://w3c.github.io/vc-data-model/)。
感谢 Manu Sporny 编写了大部分源材料，感谢 Tzviya Siegman 起草了本文档，感谢 Oliver Terbu 和 Ken Ebert 添加了可验证凭证的示例。
