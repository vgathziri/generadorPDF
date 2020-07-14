<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-btn text @click="generarFormato()">
        <span class="mr-2">FORMATO</span>
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn text @click="generarReferencia()">
        <span class="mr-2">REFERENCIA</span>
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn text @click="generarInstrumento()">
        <span class="mr-2">INSTRUMENTO</span>
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn text @click="generarDesistimiento()">
        <span class="mr-2">DESISTIMIENTO</span>
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn text @click="generarConstancia()">
        <span class="mr-2">CONSTANCIA</span>
      </v-btn>
    </v-app-bar>

    <v-content></v-content>
  </v-app>
</template>

<script>
//import jsPDF from "jspdf";
//import "jspdf-autotable";
//import HummusRecipe from "hummus-recipe";
import pdfMake from "pdfmake/build/pdfmake";
import pdfFonts from "pdfmake/build/vfs_fonts";
pdfMake.vfs = pdfFonts.pdfMake.vfs;

export default {
  name: "App",

  computed: {
    formatoFecha() {
      return this.formatDate(this.fechaActual);
    }
  },

  data: () => ({
    fechaActual: new Date().toISOString().substr(0, 10),
    nombreUsuaria: "Athziri Vázquez Gervacio",
    dependencia: "Seguridad Púbica",
    hoy: new Date()
  }),
  methods: {
    generarFormato() {
      var documento = {
        content: [
          `El Salto; Jalisco a ${this.formatoFecha}`,
          `Asunto: Se deriva Caso de Violencia Peligro extremo.`,
          `Abogada Maribel Jorge Martínez.`,
          `Directora del Centro de Justicia para las Mujeres del Estado de Jalisco`,
          `Presente`,

          `Por medio del presente le envío un cordial saludo, ocasión que hago propicia para derivar a usted a la C. (nombre completo de la Usuaria), en virtud que por parte de los servicios de atención de Trabajo Social, Psicología y Asesoría Jurídica proporcionados por esta dependencia se detectó que la ciudadana en mención se encuentra en una situación de violencia “peligro extremo” en base a la aplicación del instrumento de Evaluación de la Peligrosidad de la Violencia auto-evaluación de Peligro, con la finalidad de que se pueda realizar las acciones pertinentes en base a su competencia, ya que a dicha usuaria se le dio acompañamiento a las instalaciones del Centro de Justicia para las Mujeres, con la finalidad de presentar denuncia penal correspondiente, sin embargo en seguimiento realizado se detectó que se retiró de mencionadas instalación sin la presentación de la misma. Cabe señalar que ya se ha proporcionado el servicio de consejería y acompañamiento a parte médico de lesiones, el registro fue realizado bajo el número de folio 9735.`,

          `En relación a lo ya referido en el presente documento y toda vez que la situación de la usuaria en mención es considerada de peligro extremo (morado), pongo a su consideración realizar las acciones pertinentes de atención conforme a los lineamientos establecidos en el artículo 1, 8 y demás relativos y aplicables de nuestra Carta Magna; así como en el numeral 1, 2 y demás relativos y aplicables de la Convención Interamericana para Prevenir, Sancionar  y Erradicar la Violencia contra la Mujer (Belém do Pará); así como lo previsto en los numerales 1, 2 y demás relativos y aplicables de la Convención sobre la Eliminación de todas las formas de Discriminación contra la Mujer (CEDAW); así como los establecido en los numerales 4, 8 y demás relativos y aplicables de la Constitución Política del Estado de Jalisco; así como por lo previsto por los numerales 1, 9, 10, 11, 44, 45, 45 bis, 46, 49, 49 bis, y demás relativos y aplicables de la Ley de Acceso de las Mujeres a una Vida Libre de Violencia del Estado de Jalisco; así como lo previsto por el artículo 176 ter, 188, 206 y demás relativos y aplicables del Código Penal del Estado de Jalisco, así como en lo previsto por el artículo 3, 8 y demás relativos y aplicables de la Ley Orgánica de la Fiscalía del Estado de Jalisco; así como en lo previsto por el numeral 137 del Código Nacional de Procedimientos Penales; así como en lo previsto por el Protocolo de Atención Integral del Centro de Justicia para las Mujeres del Estado de Jalisco.`,

          `El domicilio donde puede ser localizada la C.nombre de la usuaria, es en la finca marcada con el número ----- de la calle -----, en la Colonia ----, en el municipio de ------, Jalisco, entre las calles -------- y -----------. (anexo 1)`,

          `Finalmente cabe mencionar que es de suma importancia considerar el otorgamiento de las Medidas de Protección pertinentes así como las gestiones correspondientes de albergue o refugio en caso de ser necesario.`,

          `Sin más por el momento, reitero mi más distinguida consideración.`,
          `Atentamente`,
          `F I R M A S`,
          `“2020, Año de la Acción por el Clima, de la Eliminación de la Violencia contra las Mujeres y su Igualdad Salarial”`,
          `VoBo. Edgar Joel Sánchez Rodríguez, Jefe de Unidades Internas Especializadas En Atención A Mujeres Víctimas de Violencias de la Secretaría de Igualdad Sustantiva para Mujeres y Hombres del Estado de Jalisco`,
          `C.c.p.  Lcda. María Celia Córdova Briseño, Dirección de la Unidad Especializada en la Investigación de Delitos en Contra de Mujeres de la Fiscalía Estatal. C.c.p. Archivo LERH/ejsr.`,
          `* La información de este documento fue recomendada por la Secretaria de Igualdad Sustantiva entre Mujeres y Hombres del Estado de Jalisco`
        ],
        styles: {
          header: {
            fontSize: 18,
            bold: true,
            margin: [0, 0, 0, 10]
          },
          subheader: {
            fontSize: 16,
            bold: true,
            margin: [0, 10, 0, 5]
          },
          tabla: {
            margin: [0, 5, 0, 15]
          },
          tableHeader: {
            bold: true,
            fontSize: 13,
            color: "black"
          }
        },
        defaultStyle: {
          alignment: "justify"
        }
      };
      pdfMake.createPdf(documento).open();
      //pdfMake.createPdf(documento).download("CONSTANCIA DE SERVICIOS OFRECIDOS.pdf");
    },
    generarReferencia() {
      var documento = {
        content: [
          "FORMATO ÚNICO DE REFERERENCIA Y CONTRA-REFERENCIA",
          "PARA LA ATENCIÓN DE VIOLENCIA EN CONTRA DE LAS MUJERES",
          "F1. REFERENCIA",
          `De: `,
          `Para:`,
          `Trabajadora social que canalizó el caso: `,
          `Servicio o programa:`,
          `N° de canalización: _______ N° de caso o registro: ________ Fecha (dd/mm/aaaa) ________ `,
          `1. Datos de la usuaria/o`,
          `Nombre completo:`,
          `Sexo: _________		Edad: __________		Estado civil: ______________`,
          `Domicilio. Calle y número exterior e interior:`,
          `Cruza con:_____________  Colonia o comunidad:____________`,
          `Municipio:      Estado:`,
          `Teléfono particular: ______________ Teléfono recados: ___________ Nombre: ________`,
          `Nombre de la persona a cargo (en caso de que sea niña, niño o adolescentes)
          ________________________________________ Edad: _______ Parentesco: ____________`,
          `2. Descripción de la problemática:`,
          `3. Solicitud: `,
          `4. Se anexa la siguiente documentación:`,
          `5. Observaciones y sugerencias:`,
          `En caso de ser autorizado el apoyo o de requerir más información, favor de comunicarse con:`,
          `Responsable del caso: _____________________________ Al programa de: ______________`,
          `Teléfono: ____________________ Extensión: _____________ Horario: _________________`,
          `Nota: Este documento oficial tiene una vigencia de treinta días naturales a partir de la fecha de su expedición, por lo que no será válido en otras dependencias en fechas posteriores. La petición del apoyo solicitado será valorada por el área receptora de acuerdo a sus lineamientos institucionales.`,
          `Atentamente		__________________________	__________________________`,
          `Manifiesto bajo protesta de decir la verdad a proporcionar mis datos personales, así como mi aceptación del aviso de confidencialidad  en donde señala que serán resguardados conforme a la ley establecida.`,
          `Aviso de privacidad: https://www.elsalto.gob.mx/`,
          "FORMATO ÚNICO DE REFERERENCIA Y CONTRA-REFERENCIA",
          "PARA LA ATENCIÓN DE VIOLENCIA EN CONTRA DE LAS MUJERES",
          `F2 CONTRAREFERENCIA`,
          `De: `,
          `Para: `,
          `Trabajadora social que canalizó el caso:`,
          `Servicio o programa:`,
          `N° de Contra canalización: ____________ En respuesta a la canalización N°: ____________`,
          `Datos de la usuaria/o`,
          `Nombre completo:`,
          `1. Resolución o avances de la atención:`,
          `2. Responsable del caso: `,
          `Teléfono: _________________ Ext: ____________`,
          `Caso abierto: ______________ Caso cerrado: _______`,
          `Atentamente`,
          `_______________________________`,
          `Responsable de Trabajo Social`,
          `Nota: Este documento oficial tiene una vigencia de treinta días naturales a partir de la fecha de su expedición, por lo que no será válido en otras dependencias en fechas posteriores. La petición del apoyo solicitado será valorada por el área receptora de acuerdo a sus lineamientos institucionales.`,
          `Atentamente		__________________________	__________________________`,
          `Responsable de Trabajo Social			Usuaria/o`,
          `Céd. Prof.`,
          `*La información de este documento fue recomendada por la Secretaria de Igualdad Sustantiva entre Mujeres y Hombres del Estado de Jalisco`,
          `Aviso de privacidad: https://www.elsalto.gob.mx/`
        ],
        styles: {
          header: {
            fontSize: 18,
            bold: true,
            margin: [0, 0, 0, 10]
          },
          subheader: {
            fontSize: 16,
            bold: true,
            margin: [0, 10, 0, 5]
          },
          tableExample: {
            margin: [0, 5, 0, 15]
          },
          tableHeader: {
            bold: true,
            fontSize: 13,
            color: "black"
          }
        },
        defaultStyle: {
          // alignment: 'justify'
        }
      };
      pdfMake.createPdf(documento).open();
      //pdfMake.createPdf(documento).download("REFERENCIA Y CONTRAREFERENCIA.pdf");
    },
    generarInstrumento() {
      var documento = {
        content: [
          `Marque Si o No para cada una de las siguientes frases (Él, refiere para tu esposo, novio o expareja, o quien sea que frecuentemente te esté haciendo daño).`,
          {
            style: "tabla",
            table: {
              body: [
                ["Preguntas", "Si", "No"],
                [
                  "1. ¿Ha aumentado la violencia física en severidad o frecuencia, en el último año?",
                  " ",
                  " "
                ],
                ["2. ¿Tiene él algún arma?", " ", " "],
                [
                  "3. ¿Le ha dejado usted, después de vivir juntos, en el último año?\n3a. [Si nunca ha vivido con él, señálelo aquí ____]",
                  " ",
                  " "
                ],
                [
                  "4. ¿Está él en paro (desempleado, sin trabajo) actualmente?",
                  " ",
                  " "
                ],
                [
                  "5. ¿Ha usado algún arma contra usted o le ha amenazado con algún arma? \n5a. [En caso afirmativo, ¿fue con una pistola? _____]",
                  " ",
                  " "
                ],
                ["6. ¿Le ha amenazado con matarla? ", " ", " "],
                [
                  "7. ¿Ha evitado él ser arrestado por violencia doméstica?",
                  " ",
                  " "
                ],
                ["8. ¿Tiene usted algún niño/hijo que no es de él?", " ", " "],
                [
                  "9. ¿Le ha forzado a mantener relaciones sexuales cuando usted no lo deseaba?",
                  " ",
                  " "
                ],
                ["10. ¿Ha intentado alguna vez estrangularla?", " ", " "],
                [
                  "11. ¿Toma él drogas?, como por ejemplo anfetaminas, cocaína, heroína, crack u otras drogas.",
                  " ",
                  " "
                ],
                [
                  "12. ¿Es alcohólico o tiene problemas con el alcohol?",
                  " ",
                  " "
                ],
                [
                  "13. ¿Le controla él la mayoría de sus actividades diarias? Por ejemplo, le dice con quién puede hacer amistades, cuándo puede ver a su familia, cuánto dinero puede usar/gastar, o cuándo puede coger el coche. \n13a. [Si lo intenta, pero usted no le deja, señálelo aquí _____]",
                  " ",
                  " "
                ],
                [
                  "14. ¿Es celoso con usted constante y violentamente? (Por ejemplo, dice “si no puedo tenerte, nadie podrá”)",
                  " ",
                  " "
                ],
                [
                  "15. ¿Le ha golpeado alguna vez estando embarazada? \n15a. [Si no ha estado nunca embarazada de él, señálelo aquí ____]",
                  " ",
                  " "
                ],
                [
                  "16. ¿Alguna vez él ha amenazado con suicidarse o lo ha intentado?",
                  " ",
                  " "
                ],
                ["17. ¿Amenaza él con hacer daño a sus hijos? ", " ", " "],
                ["18. ¿Cree usted que es capaz de matarla?", " ", " "],
                [
                  "19. ¿La persigue o espía, le deja notas amenazantes o mensajes en el contestador, destruye sus cosas o propiedades, o le llama cuando usted no quiere?",
                  " ",
                  " "
                ],
                [
                  "20.¿Alguna vez ha amenazado usted con suicidarse o lo ha intentado?",
                  " ",
                  " "
                ]
              ]
            }
          },
          `Total, de respuestas (Sí es): ……………. `,
          `Gracias. Por favor, consulte con su enfermera o consejero las implicaciones que el Auto-Evaluación de Riesgo tiene para usted.`,
          `Estimación de la Evaluación de Peligro: `,
          {
            ul: [
              "Sume el número total de “sí es” de 1 a 20",
              "Sume 4 puntos por cada “sí” a las preguntas 2 y 3",
              "Sume 3 puntos por el “sí” a la pregunta 4",
              "Sume 3 puntos por los “sí es” a las preguntas a 5, 6 y 7",
              "Sume 1 punto por cada “sí” a las preguntas 8 y 9",
              "Reste 3 puntos si la opción 3a fue seleccionada"
            ]
          },
          `Basándose en las puntuaciones obtenidas, la Estimación de Peligro sería: ____`,
          {
            ul: [
              "Una puntuación menor de 8 indicaría “Peligro Variable” correspondiente a color “VERDE”. Informe a la mujer que el nivel de peligro puede cambiar de forma rápida y que, por lo tanto, ha de estar alerta a otros signos de peligro, dígale que confíe en su instinto (señales físicas de su cuerpo)",
              "Una puntuación entre 8 y 13 indicaría “Aumento del Peligro” correspondiente a color “AMARILLO”. Advierta a la mujer del riesgo, aconseje un plan de seguridad; sugiera consejo legal y supervise con atención las recomendaciones hechas.",
              "Una puntuación entre 14 y 17 indicaría “Peligro Severo” correspondiente a color “ROJO”. Advierta a la mujer del riesgo, aconseje un plan de seguridad; sugiera consejo legal y supervise con atención las recomendaciones hechas.",
              "Una puntuación por encima de 18 indicaría “Peligro Extremo” correspondiente a color “MORADO”. Advierta a la mujer del serio peligro que corre, han de tomarse decisiones contundentes e inmediatas: denuncia ante la autoridad competente o a otros profesionales que puedan ayudar, valorar situación de apoyos con redes de la persona atendida y en su caso resguardar en albergue o refugio."
            ]
          },
          `*La información de este documento fue recomendada por la Secretaria de Igualdad Sustantiva entre Mujeres y Hombres del Estado de Jalisco`
        ],
        styles: {
          header: {
            fontSize: 18,
            bold: true,
            margin: [0, 0, 0, 10]
          },
          subheader: {
            fontSize: 16,
            bold: true,
            margin: [0, 10, 0, 5]
          },
          tabla: {
            margin: [0, 5, 0, 15]
          },
          tableHeader: {
            bold: true,
            fontSize: 13,
            color: "black"
          }
        },
        defaultStyle: {
          alignment: "justify"
        }
      };
      pdfMake.createPdf(documento).open();
      //pdfMake.createPdf(documento).download("INSTRUMENTO DE VALORACIÓN DA.pdf");
    },
    generarDesistimiento() {
      var horaActual = this.hoy.getHours() + ":" + this.hoy.getMinutes();
      var documento = {
        header: {text: 'DAMVV/SEM.ELSALTO/003', alignment:"right",margin:[0,0,20,0]},

        footer: {
          columns: [{text: `*La información de este documento fue recomendada por la Secretaria de Igualdad Sustantiva entre Mujeres y Hombres del Estado de Jalisco`,margin: [20, 0, 20, 0], fontSize: 10,}]
        },
        content: [
          { text: "CONSTANCIA DE DESISTIMIENTO DE SERVICIOS", style: "header"},
          { text: `\nFecha: ${this.formatoFecha}.    Hora: ${horaActual}.    Folio: ____`, alignment:"right", margin:[0,0,20,0]},
          `Yo ${this.nombreUsuaria} encontrándome en pleno uso y goce de mis facultades y libre de cualquier coacción, es mi decisión y por así convenir a mis intereses no aceptar en este momento los servicios de apoyo, traslado y/o acompañamiento que se me ofrecen en este instante:`,

          {
            style: "tabla",
            widths: [100, "*", 100, "*", 100, "*"],
            table: {
              body: [
                [
                  "Parte médico de lesiones",
                  " ",
                  "Acompañamiento a  Centro de Justicia para las Mujeres",
                  " ",
                  "Acompañamiento a Ciudad Niñez",
                  " "
                ],
                [
                  "Orden de protección en domicilio particular",
                  " ",
                  "Red de apoyo",
                  " ",
                  "Acompañamiento a Ministerio Público",
                  " "
                ],
                [
                  "Refugio/albergue",
                  " ",
                  "Orden de protección",
                  " ",
                  "Asesoría Jurídica",
                  " "
                ]
              ]
            }
          },
          `Por lo que deslindo de cualquier responsabilidad administrativa, civil o penal a El Gobierno Municipal de El Salto, Jalisco.`,
          `Dicho lo anterior, me responsabilizo de mi decisión pese a que por parte del personal especializado que me ha atendido, se me ha hecho saber el riesgo inminente en mi integridad física y/o psicológica por parte del generador de violencia. Aun así y a sabiendas de ello, es mi deseo retirarme de esta Dependencia sin haber aceptado dicho apoyo.`,
          `Exposición de Motivos: `,
          `*La información de este documento fue recomendada por la Secretaria de Igualdad Sustantiva entre Mujeres y Hombres del Estado de Jalisco`,
          `Nombre y firma de la usuaria 	   	                      Huella`,
          `Trabajo social		                           Psicología		             		     Jurídico`,

          `Nombre y firma de quien/es brindaron la orientación/atención y número de Cédula Profesional.`
        ],
        styles: {
          header: {
            fontSize: 12,
            bold: true,
            alignment: "center",
            margin: [0, 20, 0, 0]
          },
          parrafo: {
            fontSize: 12,
            alignment: "justify",
            margin: [25, 0, 25, 0]
          },
          tabla: {
            margin: [25, 20, 25, 0]
          }
        },
        defaultStyle: {
          alignment: "justify"
        }
      };
      pdfMake.createPdf(documento).open();
      //pdfMake.createPdf(documento).download("CONSTANCIA DE DESISTIMIENTO DE SERVICIOS.pdf");
    },

    generarConstancia() {
      var horaActual = this.hoy.getHours() + ":" + this.hoy.getMinutes();
      var documento = {
        footer: {
          columns: [{text: `*La información de este documento fue recomendada por la Secretaria de Igualdad Sustantiva entre Mujeres y Hombres del Estado de Jalisco`,margin: [20, 0, 20, 0], fontSize: 10,}]
        },
        content: [
          { text: "CONSTANCIA DE SERVICIOS OFRECIDOS", style: "header" },
          {
            text: `\nFecha: ${this.formatoFecha}. Hora: ${horaActual}`,
            alignment: "right",
            margin: [0, 0, 20, 0]
          },
          { text: `Folio: _____`, alignment: "right", margin: [0, 0, 20, 0] },

          {
            text: `\nYo ${this.nombreUsuaria} manifiesto que, por parte de ${this.dependencia} recibí Atención haciéndome entrega de un plan de seguridad, se me explicó los tipos y modalidades de violencia, ciclo de violencia y el nivel de riesgo en el que me encuentro actualmente, además de las recomendaciones inmediatas a realizar de acuerdo a mi situación particular.`,
            style: "parrafo"
          },
          {
            text: `\nAsimismo, refiero que por parte de esta dependencia recibí los servicios de apoyo, traslado y/o acompañamiento que se me ofrecen en este instante:\n`,
            style: "parrafo"
          },
          {
            style: "tabla",
            widths: ["auto", "*", "auto", "*", "auto", "*"],
            table: {
              body: [
                [
                  "Parte médico de lesiones",
                  " ",
                  "Acompañamiento a  Centro de Justicia para las Mujeres",
                  " ",
                  "Acompañamiento a Ciudad Niñez",
                  " "
                ],
                [
                  "Orden de protección en domicilio particular",
                  " ",
                  "Red de apoyo",
                  " ",
                  "Acompañamiento a Ministerio Público",
                  " "
                ],
                [
                  "Refugio/albergue",
                  " ",
                  "Orden de protección",
                  " ",
                  "Asesoría Jurídica",
                  " "
                ],
                [
                  "Asesoría Psicológica",
                  " ",
                  { colSpan: 4, rowSpan: 1, text: "Otro especifique" },
                  "",
                  "",
                  ""
                ]
              ]
            }
          },
          {
            text: `\nFinalmente, y bajo protesta de decir verdad, se me recomienda y se me hace ver la importancia de presentar denuncia penal por la situación de riesgo eminente, por la que me comprometo a realizar dicho trámite.`,
            style: "parrafo"
          },
          {
            text: `\nEn razón de lo anterior, me retiro de esta Dependencia conforme con los servicios que me han ofrecido.`,
            style: "parrafo"
          },
          {
            text: `\n\n\n_______________________________________   		___________`,
            alignment: "center"
          },
          {
            text: `Nombre y firma de la usuaria   	                    	Huella`,
            alignment: "center",
            fontSize: 11
          },
          {
            text: `\n\n____________________________________  	       	____________________________________`,
            alignment: "center"
          },
          {
            text: `Trabajo social   	                                                      	Psicología`,
            alignment: "center",
            fontSize: 11
          },
          {
            text: `\n\n____________________________________  	       	____________________________________`,
            alignment: "center"
          },
          {
            text: `Jurídico   	                                                           	Medica(o)`,
            alignment: "center",
            fontSize: 11
          },
          {
            text: `\n\n____________________________________`,
            alignment: "center"
          },
          { text: `Elemento operativo`, alignment: "center", fontSize: 11 },
          {
            text: `\n\n_________________________________________________________________________________`,
            alignment: "center"
          },
          {
            text: `Nombre y firma de quien brindó la  orientación/atención y número de Cédula Profesional`,
            alignment: "center",
            fontSize: 11
          },
         
        ],
        styles: {
          header: {
            fontSize: 12,
            bold: true,
            alignment: "center",
            margin: [0, 20, 0, 0]
          },
          parrafo: {
            fontSize: 12,
            alignment: "justify",
            margin: [25, 0, 25, 0]
          },
         
          tabla: {
            margin: [25, 20, 25, 0]
          }
        },
        defaultStyle: {
          alignment: "justify"
        }
      };
      //pdfMake.createPdf(documento).open();
      pdfMake.createPdf(documento).download("CONSTANCIA DE SERVICIOS OFRECIDOS.pdf");
    },
    formatDate(date) {
      if (!date) return null;
      const [year, month, day] = date.split("-");
      this.fechaActual = `${day}/${month}/${year}`;
      return `${day}/${month}/${year}`;
    }
  }
};
</script>
