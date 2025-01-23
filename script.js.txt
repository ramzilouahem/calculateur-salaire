function calculateSalary() {
    const baseSalary = parseFloat(document.getElementById('baseSalary').value) || 0;
    const ptp = parseFloat(document.getElementById('ptp').value) || 0;
    const nuisance = parseFloat(document.getElementById('nuisance').value) || 0;
    const responsibility = parseFloat(document.getElementById('responsibility').value) || 0;
    const itp = parseFloat(document.getElementById('itp').value) || 0;
    const ifsp = parseFloat(document.getElementById('ifsp').value) || 0;
    const differentialIncome = parseFloat(document.getElementById('differentialIncome').value) || 0;
    const performanceBonus = parseFloat(document.getElementById('performanceBonus').value) || 0;
    const encouragementBonus = parseFloat(document.getElementById('encouragementBonus').value) || 0;

    const entryDate = new Date(document.getElementById('entryDate').value);
    const currentDate = new Date();

    if (isNaN(entryDate)) {
        alert("Veuillez saisir une date d'entrée valide.");
        return;
    }

    // Calcul de l'IEP
    let experienceYears = currentDate.getFullYear() - entryDate.getFullYear();
    if (currentDate.getMonth() < entryDate.getMonth() || 
        (currentDate.getMonth() === entryDate.getMonth() && currentDate.getDate() < entryDate.getDate())) {
        experienceYears--;
    }

    const iep = experienceYears > 0 ? experienceYears * 1000 : 0;

    // Calcul du Salaire de Poste
    const posteSalary = baseSalary + ptp + nuisance + responsibility + itp + ifsp + differentialIncome + iep + performanceBonus + encouragementBonus;

    // Retenue Sécurité Sociale
    const securitySocialDeduction = posteSalary * 0.09;

    // Base Imposable IRG
    const taxableBase = posteSalary - securitySocialDeduction;

    // Calcul de la Retenue IRG selon le barème 2022
    let retenueIRG = 0;
    if (taxableBase > 320000) retenueIRG += (taxableBase - 320000) * 0.35;
    if (taxableBase > 192000 && taxableBase <= 320000) retenueIRG += (taxableBase - 192000) * 0.33;
    if (taxableBase > 96000 && taxableBase <= 192000) retenueIRG += (taxableBase - 96000) * 0.30;
    if (taxableBase > 48000 && taxableBase <= 96000) retenueIRG += (taxableBase - 48000) * 0.27;
    if (taxableBase > 24000 && taxableBase <= 48000) retenueIRG += (taxableBase - 24000) * 0.23;

    // Salaire Net
    const netSalary = taxableBase - retenueIRG;

    // Masse Salariale
    const salaryMass = posteSalary + posteSalary * 0.35;

    // Affichage des résultats
    document.getElementById('iepValue').textContent = iep.toFixed(2) + " DA";
    document.getElementById('posteSalary').textContent = posteSalary.toFixed(2) + " DA";
    document.getElementById('securitySocialDeduction').textContent = securitySocialDeduction.toFixed(2) + " DA";
    document.getElementById('taxableBase').textContent = taxableBase.toFixed(2) + " DA";
    document.getElementById('irgDeduction').textContent = retenueIRG.toFixed(2) + " DA";
    document.getElementById('netSalary').textContent = netSalary.toFixed(2) + " DA";
    document.getElementById('salaryMass').textContent = salaryMass.toFixed(2) + " DA";
}

    // Affichage des résultats
    document.getElementById('iepValue').textContent = iep.toFixed(2) + " DA";
    document.getElementById('posteSalary').textContent = posteSalary.toFixed(2) + " DA";
    document.getElementById('securitySocialDeduction').textContent = securitySocialDeduction.toFixed(2) + " DA";
    document.getElementById('taxableBase').textContent = taxableBase.toFixed(2) + " DA";
    document.getElementById('irgDeduction').textContent = retenueIRG.toFixed(2) + " DA";
    document.getElementById('netSalary').textContent = netSalary.toFixed(2) + " DA";
    document.getElementById('salaryMass').textContent = salaryMass.toFixed(2) + " DA";
}
