# Framework-de-Avalia-o-de-Seguran-a-de-Fornecedores-TPRM-
Questionário de Auditoria (VSA - Vendor Security Assessment)

def avaliar_fornecedor(respostas):
    score = 0
    criterios_obrigatorios = ["Criptografia_Dados", "Backup_Imutavel", "Certificacao_ISO27001"]
    
    # Verifica itens eliminatórios para o setor bancário
    for item in criterios_obrigatorios:
        if respostas.get(item) == "Não":
            return "❌ REJEITADO: Falta requisito obrigatório de conformidade BACEN."
    
    # Pontuação baseada em boas práticas
    score += 40 if respostas.get("MFA_Obrigatorio") == "Sim" else 0
    score += 30 if respostas.get("Seguro_Ciber") == "Sim" else 0
    score += 30 if respostas.get("Pentest_Anual") == "Sim" else 0

    if score >= 70:
        return f"✅ APROVADO: Score {score}/100. Fornecedor de Baixo Risco."
    return f"⚠️ ATENÇÃO: Score {score}/100. Requer análise do Comitê de Risco."

# Simulação de auditoria de um fornecedor de Cloud do BV
fornecedor_x = {
    "Criptografia_Dados": "Sim",
    "Backup_Imutavel": "Sim",
    "Certificacao_ISO27001": "Sim",
    "MFA_Obrigatorio": "Sim",
    "Seguro_Ciber": "Não",
    "Pentest_Anual": "Não"
}

print(f"Resultado da Avaliação: {avaliar_fornecedor(fornecedor_x)}")
