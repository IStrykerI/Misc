#
# This is a Shiny web application. You can run the application by clicking
# the 'Run App' button above.
#
# Find out more about building applications with Shiny here:
#
#    http://shiny.rstudio.com/
#

# Libraries Used ----
library(shiny)
library(shinyFiles)
library(shinythemes)
library(shinyWidgets)

# UI -----------------------------------------------------------------------------------------------

# Define UI for data upload app ----
ui <- navbarPage("Misc App", theme = shinytheme("cyborg"), 
                 tabPanel("Multi File Renaming",
                          sidebarPanel(
                            actionButton("refresh", "Refresh Display"),
                            hr(),
                            textInput("from", "From Name Pattern:", value = ""),
                            textInput("to", "To name Pattern:", value = ""),
                            actionButton("preview", "Preview Changes"),
                            actionButton("change", "Rename")
                          ),
                          # Main panel for displaying outputs ----
                          mainPanel(
                            h4("Current Files"),
                            verbatimTextOutput("dirFiles"), 
                            h4("Preview Changes to Files"),
                            verbatimTextOutput("fileChanges"), 
                            br(),
                            # App Background ----
                            setBackgroundImage(src = "https://d2v9y0dukr6mq2.cloudfront.net/video/thumbnail/GfRLKaE/videoblocks-abstract-scifi-tech-background_h8m3zcivm_thumbnail-full14.png"),
                            width = 10
                          )
                 )
)


# End of UI ----------------------------------------------------------------------------------------

# Server -------------------------------------------------------------------------------------------

# Define server logic to read selected file ----
server <- function(input, output, session) {
  output$dirFiles <- renderPrint(list.files())
  
  observeEvent(input$change, {
    file_names = list.files()
    if (grepl("\\(", input$from)) {
      file_names_change = gsub("\\(", input$to, file_names)
    }
    else if (grepl("\\)", input$from)) {
      file_names_change = gsub("\\)", input$to, file_names)
    }
    else {
      file_names_change = gsub(input$from, input$to, file_names)
    }
    result = file.rename(list.files(), file_names_change)
    output$dirFiles <- renderPrint(list.files())
  })
  
  observeEvent(input$preview, {
    file_names = list.files()
    if (grepl("\\(", input$from)) {
      file_names_change = gsub("\\(", input$to, file_names)
    }
    else if (grepl("\\)", input$from)) {
      file_names_change = gsub("\\)", input$to, file_names)
    }
    else {
      file_names_change = gsub(input$from, input$to, file_names)
    }
    output$fileChanges <- renderPrint(file_names_change)
  })
  
  observeEvent(input$refresh, {
    session$reload()
    return()
  })
}

# End of Server ------------------------------------------------------------------------------------

# Launches UI and server ----
shinyApp(ui, server)