---

copyright:
  years: 2019
lastupdated: "2019-06-27"

subcollection: speech-to-text-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Gestion du cluster
{: #manage}

Après avoir installé et configuré {{site.data.keyword.speechtotextdatafull}} sur {{site.data.keyword.icp4dfull}}, vous pouvez gérer l'instance et le cluster.

## Préparation de votre machine locale
{: #manage-prep-local-machine}

Vérifiez que les prérequis suivants sont installés et fonctionnent correctement sur votre machine locale avant d'effectuer des tâches de gestion de cluster.

1. Installez et configurez les outils de ligne de commande suivants :

  - {{site.data.keyword.icp4dfull_notm}} 2.1.0 ou version ultérieure, y compris l'interface de ligne de commande IBM Cloud Private : [`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - Kubernetes 1.12.4 ou version ultérieure : [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - Helm 2.9.1 ou version ultérieure : [`helm`](https://helm.sh){: external}

1.  Démarrez `helm` :

    ```bash
    helm init --client-only
    ```
    {: pre}

1.  Vérifiez que les outils sont installés correctement en exécutant les commandes de test suivantes.

    - Testez l'interface de ligne de commande IBM Cloud Private (`cloudctl`) :

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
      ```
      {: pre}

      Si vous utilisez un équilibreur de charge, indiquez le nom d'hôte de l'équilibreur de charge au lieu du nom d'hôte du noeud maître.
      {: note}

    - Testez Kubernetes (`kubectl`) :

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      Si vous ne pouvez pas exécuter la commande `kubectl`, voir [Activation de l'accès à l'interface de ligne de commande Kubernetes](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}.
      {: note}

    - Testez Helm (`helm`) :

      ```bash
      helm version --tls
      ```
      {: pre}

## Exécution de tâches de gestion
{: perform-mgmt-tasks}

Voici quelques tâches que vous pouvez effectuer pour surveiller et gérer votre instance {{site.data.keyword.speechtotextshort}}.

  - Identifiez les noeuds de cluster sur lesquels le produit est déployé :
```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - Répertoriez le nombre de répliques de chaque microservice dans un `{namespace}` donné :

```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    ou
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - Modifiez (augmentez ou diminuez) le nombre de répliques :

```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    ou
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - Affichez les journaux

    Par défaut, {{site.data.keyword.icp4dfull_notm}} consigne automatiquement les informations de chaque service. Pour plus d'informations, voir [Affichage des journaux](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}.

## Gestion de l'accès utilisateur
{: #manage-user-access}

Après avoir mis à disposition une instance, vous pouvez partager l'URL du service avec d'autres utilisateurs. Toutefois, ces utilisateurs ne peuvent se connecter au service que si vous leur octroyez l'accès.

Si vous prévoyez d'utiliser SAML pour la connexion unique (SSO), effectuez la [Configuration de la connexion unique (SSO)](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso) avant d'ajouter des utilisateurs. Si vous ajoutez des utilisateurs avant de configurer SSO, vous devez réajouter les utilisateurs avec leurs ID SAML pour leur permettre d'utiliser la connexion unique.

1.  Dans le menu du client Web, cliquez sur **Administrer > Gérer un utilisateur**.

1.  Cliquez sur **Ajouter un utilisateur**, puis indiquez le nom complet de l'utilisateur, le nom d'utilisateur et l'adresse électronique de l'utilisateur. Définissez les droits de l'utilisateur, puis cliquez sur **Ajouter**.

1.  Dans le menu du client Web, sélectionnez **Mes instances**.

1.  Recherchez votre instance {{site.data.keyword.speechtotextshort}}, cliquez sur le menu d'options supplémentaires (**...**), puis sélectionnez **Gérer l'accès**.

1.  Cliquez sur **Ajouter un utilisateur**.

1.  Cliquez sur la zone de nom d'utilisateur pour afficher la liste des personnes que vous pouvez ajouter.

    Les utilisateurs que vous avez ajoutés aux étapes précédentes sont répertoriés. Sélectionnez un nom, choisissez **Utilisateur** ou **Admin** en tant que rôle d’accès, puis cliquez sur **Ajouter**.

    Si vous n'êtes pas connecté à un registre d'utilisateurs existant et que vous n'avez pas activé la connexion unique, des mots de passe temporaires sont créés pour les utilisateurs que vous ajoutez. Les mots de passe temporaires sont envoyés aux utilisateurs via les adresses électroniques que vous avez spécifiées.
